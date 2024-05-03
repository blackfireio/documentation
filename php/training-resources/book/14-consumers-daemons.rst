Chapter 14 - Profiling Consumers
================================

Blackfire can be used to profile anything, from incoming HTTP requests to
executed CLI scripts, but what about consumers and daemons? Relying on
Blackfire's auto-instrumentation for consumers and daemons is impossible, since
they run for a very long period of time. If a script never ends, the profile
will never be complete and will never show up on Blackfire.

Most of the time, long running scripts are consumers: they consume messages from
a queue or read messages from a database.

Profiling a consumer commonly consists of instrumenting the code executed in
the main loop. There are many possible profiling strategies, depending on what
your consumer does and the kinds of messages it deals with.

.. sidebar:: Never-ending PHP Consumers as Daemons

    Consumers written in PHP can be written with the following:

    .. code-block:: php

        // create an infinite loop
        while (true) {
            // do something
        }

    The above code runs indefinitely **in the foreground**. To make it a "real"
    daemon and run your PHP consumer in the background, use standard Unix tools
    like Upstart.

Installing the PHP SDK
----------------------

The Blackfire PHP SDK provides a nice API that, amongst other things, gives
you access to the Blackfire PHP instrumentation triggering system.

All you need to get started is to install the SDK via Composer:

.. code-block:: bash

    composer require blackfire/php-sdk

.. note::

    Do not add Blackfire's SDK as a dev dependency (``--dev``) as code relying
    on it should work in production as well.

Using the PHP SDK
-----------------

Create a ``consumer.php`` file with the following content:

.. code-block:: php
    :emphasize-lines: 10,12,16

    require_once __DIR__.'/vendor/autoload.php';

    use Blackfire\Client;

    function consume()
    {
        echo "Message consumed!\n";
    }

    $blackfire = new Client();

    $probe = $blackfire->createProbe();

    consume();

    $profile = $blackfire->endProbe($probe);

    print $profile->getUrl()."\n";

Run it like any regular PHP script:

.. code-block:: php

    php consumer.php

The ``Blackfire\Client`` instance created on line 10 is the main SDK entry
point. To profile a piece of code, wrap it with ``createProbe()`` (line 12) and
``endProbe()`` (line 16). Line 18 displays the URL where you can access the
generated profile.

Some major differences between auto-instrumentation and using the SDK:

* The SDK allows you to create several profiles from one script execution
  (create several probes);

* The SDK returns the profile as an object, giving you the opportunity to get
  profiling data right in the script (which you might use to make decisions);

* The SDK gathers less information as it hooks into the PHP engine much later
  and leaves much sooner than when auto-instrumentation is used (even if
  ``createProbe()`` and ``endProbe()`` are the very first and the very last
  line of the script);

* To run the script, **do not** use ``blackfire run`` as instrumentation and
  profile generation is triggered directly from the code itself (the Blackfire
  command line tool main responsibility is to generate a signature, which is
  done when calling the PHP SDK ``createProbe()`` method).

Instrumenting a Consumer
------------------------

A naive implementation of a consumer might profile all consumed messages:

.. code-block:: php

    $blackfire = new Client();

    while (true) {
        $probe = $blackfire->createProbe();

        consume();

        $profile = $blackfire->endProbe($probe);

        print $profile->getUrl()."\n";

        usleep(10000);
    }

This implementation suffers from several problems:

* On busy consumers, this code will generate tons of profiles that nobody will
  ever look at;

* The code is not optimal as all message consumptions are affected by
  Blackfire's overhead;

* Each profile leads to several HTTP round-trips to Blackfire's servers,
  slowing down the consumer significantly;

If all consumed messages are of the same type you can use the PHP SDK to
aggregate several messages into one profile:

.. code-block:: php

    require_once __DIR__.'/vendor/autoload.php';

    use Blackfire\Client;
    use Blackfire\Profile\Configuration as ProfileConfiguration;

    function consume()
    {
        echo "Message consumed!\n";
    }

    $blackfire = new Client();
    $maxIterations = 10;
    $currentIteration = 0;
    $profileConfig = new ProfileConfiguration();
    $profileConfig->setTitle('Consumer')->setSamples($maxIterations);

    while (true) {
        if (0 === $currentIteration) {
            $probe = $blackfire->createProbe($profileConfig, false);
        }

        $probe->enable();

        consume();

        $probe->close();

        ++$currentIteration;
        if ($currentIteration === $maxIterations) {
            $profile = $blackfire->endProbe($probe);
            $currentIteration = 0;

            print $profile->getUrl()."\n";
        }

        usleep(10000);
    }

There is a lot going on here. Let's describe the code in more detail:

* Line 14: Create a ``Blackfire\Profile\Configuration`` instance that holds
  profile configuration: the number of iterations for each profile (``10``) and
  the profile title (``Consumer``);

* Lines 18-20: The probe does not exist yet or a profile has just been
  generated in the previous iteration, create a new profile (``false`` disables
  probe auto-start);

* Line 22: Starts a new iteration for the current profile;

* Line 26: Stops the iteration;

* Line 31-33: The max iterations is reached, end the profile and send the data
  back to Blackfire.

The output should look like the following:

.. code-block:: text

    Message consumed!
    Message consumed!
    Message consumed!
    Message consumed!
    Message consumed!
    Message consumed!
    Message consumed!
    Message consumed!
    Message consumed!
    Message consumed!
    https://blackfire.io/profiles/602e1a37-b7e4-46d5-838c-ac8da38d9006/graph
    Message consumed!
    Message consumed!
    Message consumed!
    Message consumed!
    Message consumed!
    Message consumed!
    Message consumed!
    Message consumed!
    Message consumed!
    Message consumed!
    https://blackfire.io/profiles/a027fb95-2c03-470f-8184-e9af6a1cdd14/graph

This is better but not perfect, as we are still profiling all messages. What
about profiling only some messages? Like 1% of all messages, or 10 messages
every hour?

As an exercise, modify the code to generate a profile of 10 messages in a row
every 1,000 messages.

.. note::

    If the Blackfire C extension is not available on all your machines, make
    the Blackfire code conditional with the following condition:

    .. code-block:: php

        if (extension_loaded('blackfire')) {
            // do something related to Blackfire
        }

Using the PHP's SDK ``LoopClient``
----------------------------------

The last example contains a lot of boilerplate code that can be avoided by
using Blackfire's ``LoopClient`` class:

.. code-block:: php

    require_once __DIR__.'/vendor/autoload.php';

    use Blackfire\LoopClient;
    use Blackfire\Client;
    use Blackfire\Profile\Configuration as ProfileConfiguration;

    function consume()
    {
        echo "Message consumed!\n";
    }

    $blackfire = new LoopClient(new Client(), 10);
    $profileConfig = new ProfileConfiguration();
    $profileConfig->setTitle('Consumer');

    while (true) {
        $blackfire->startLoop($profileConfig);

        consume();

        if ($profile = $blackfire->endLoop()) {
            print $profile->getUrl()."\n";
        }

        usleep(400000);
    }

The ``LoopClient`` constructor takes a Blackfire ``Client`` instance and the
number of iterations for each profile. The ``startLoop()`` and ``endLoop()``
methods have the same logic as the code from before.

.. tip::

    Profiling a consumer continuously is probably never a good idea. Instead,
    trigger profiles from the outside using :ref:`signals <php-sdk-signals>`.

Conclusion
----------

Most PHP users fear consumers written in PHP as they are seen as convoluted
black boxes. Not anymore. With Blackfire's PHP SDK and only a few small
changes, you can now better understand your consumers and probably optimize
them.

The ability to manually instrument code with the Blackfire PHP SDK opens up a
lot of opportunities. One of them is the integration of Blackfire in your unit
test suite, which is our next topic.
