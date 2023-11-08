Chapter 17 - Doing more with the SDK
====================================

The PHP SDK allows to programmatically control Blackfire. We have already
covered how to leverage the SDK in unit tests and how to use the SDK to profile
consumers and daemons in previous chapters. This chapter outlines several
advanced usages of the PHP SDK. Hopefully these examples will inspire you to
create your own implementations. Your imagination is really the only limit here.

Monitoring Consumers Performance
--------------------------------

In a :doc:`previous chapter <14-consumers-daemons>`, we used the ``LoopClient``
class to instrument consumers:

.. code-block:: php

    while (true) {
        $blackfire->startLoop($profileConfig);

        consume();

        $blackfire->endLoop();

        usleep(400000);
    }

If you read the :ref:`documentation about how to profile consumers
<php-sdk-profiling-consumers-daemons>`, you should be familiar with using
signals to instrument your production code. It works like this:

.. code-block:: php

    use Blackfire\LoopClient;

    $blackfire = new LoopClient(new Client(), 10);
    $blackfire->setSignal(SIGUSR1);

* When you start the consumer process, it behaves as usual with **no
  overhead**: Blackfire does not instrument the code and the calls to
  ``startLoop()`` and ``endLoop()`` are effectively no-ops. This is **perfect
  for production**.

* When the process receives the configured signal (``SIGUSR1`` in the example),
  Blackfire instruments the code for the next ``10`` iterations (as configured
  above), generates a profile, and disables instrumentation again.

  When Blackfire's servers receive the profile, associated **tests are run**.

Whenever you want to better understand the status of one of your consumers,
signal it once and be done. That gives you on-demand profiles, but how can you
achieve periodic builds for consumers? As you might have guessed, this is a
matter of configuring a cron job:

.. code-block:: text

    # generate a profile every hour
    0 * * * * pkill -SIGUSR1 -f consumer.php

If you want to be notified whenever some tests fail, create builds and configure
a notification channel to receive build statuses and reports.

The PHP SDK provides everything you need to start builds programmatically (see
below), but ``LoopClient`` makes it even easier. Call ``generateBuilds()`` and
pass it the environment name or UUID:

.. code-block:: php

    $blackfire->generateBuilds('ENV_NAME_OR_UUID');

And you have it: **a fully automated way to continuously profile consumers**,
monitor their intrinsic performance, and their performance evolution over time.

Instrumenting Code Manually
---------------------------

When using the browser extension or the Blackfire CLI tool to trigger a profile,
there is no need to change the code. Blackfire takes care of everything for you.
But what if you want to profile only part of the executed code? That's possible
by explicitly marking the code you want to profile.

.. caution::

    Do not confuse using the PHP SDK to **manually create profiles** (which does
    not need the browser extension or the CLI tool) with manually instrumenting
    the code with the SDK, which helps Blackfire generate precise profiles when
    triggered by the browser extension or CLI tool.

First, retrieve the current probe:

.. code-block:: php

    // Get the probe main instance
    $probe = \BlackfireProbe::getMainInstance();

Then, call ``enable()`` to start the profiling and ``disable()`` to stop it:

.. code-block:: php

    // start profiling the code
    $probe->enable();

    // code that you want to profile

    // stop the profiling
    $probe->disable();

.. tip::

    You do not need to install the Blackfire SDK to benefit from this feature
    as the ``BlackfireProbe`` class is part of the Blackfire C extension.

You can mark as many sections as you want, but be warned that all sections are
going to be part of the same call graph. Including too many unrelated sections
will generate a convoluted, useless profile.

As soon as you explicitly call ``enable()`` in your code, Blackfire understands
that you want to control what to instrument and disables auto-instrumentation.

As with auto-instrumentation, profiling is only active when the code is run
through the browser extension or the Blackfire CLI utility. If a profile has not
been triggered, calls to the probe are just ignored.

.. sidebar:: Profiling HTTP Controllers

    Web frameworks provide a common abstraction to handle HTTP requests that
    can be quite noisy on a call graph. When debugging a performance issue, you
    might want to focus on the executed controller code only. Using manual
    instrumentation can be useful; here is an example of a PSR-7 middleware
    that you can use with `Zend Expressive
    <https://github.com/zendframework/zend-expressive>`_:

    .. code-block:: php

        use Psr\Http\Message\ResponseInterface;
        use Psr\Http\Message\ServerRequestInterface;
        use Zend\Stratigility\MiddlewareInterface;

        class BlackfireMiddleware implements MiddlewareInterface
        {
            public function __invoke(ServerRequestInterface $request, ResponseInterface $response, callable $out = null)
            {
                $probe = null;
                if (class_exists('BlackfireProbe', false)) {
                    $probe = BlackfireProbe::getMainInstance();
                }

                if (null !== $out) {
                    $probe and $probe->enable();
                    $response = $out($request, $response);
                    $probe and $probe->close();
                }

                return $response;
            }
        }

.. sidebar:: Profiling ReactPHP Servers

    The same technique can be used to profile HTTP requests handled by PHP
    servers like `ReactPHP <https://reactphp.org/>`_. Blackfire's PHP SDK
    provides a helper class to ease the integration, which is detailed in `this
    blog post <https://blog.blackfire.io/profiling-react-php-requests.html>`_.

Instrumenting Outgoing API Calls
--------------------------------

Some projects consist of a set of micro-services written in PHP, all
communicating via HTTP. When profiling a user-facing HTTP request for such a
project, the call graph contains many HTTP calls for which Blackfire only
displays the URL and the wall time. If one of the requests is slow, you need to
manually trigger another profile against that micro-service in order to
understand the bottlenecks.

Wouldn't it be great if you could automatically generate profiles for these API
calls? The implementation depends on the HTTP library you are using to make
your API calls, but the general idea looks like this:

.. code-block:: php

    $probe = \BlackfireProbe::getMainInstance();

    if ($probe->getResponseLine()) {
        $client = new \Blackfire\Client();

        $request = $client->createRequest();
        $header = 'X-Blackfire-Query: '.$request->getToken();

        // add the header to the external HTTP request call
    }

* *Line 1*: Get the probe for the current HTTP request;

* *Line 3*: Make sure that a profile was actually requested - if not, there is
  nothing to do;

* *Line 6*: Create a new profile request;

* *Line 7*: Generate an HTTP header containing the signature needed to trigger
  a new profile;

* *Line 9*: Finally, add this header to the outgoing request to trigger an
  additional profile for the sub-request.

.. tip::

    If you are using Guzzle, you can simplify the code as Blackfire provides a
    `native integration <https://blackfire.io/docs/php/integrations/guzzle>`_:

    .. code-block:: php

        $options = array();

        $probe = \BlackfireProbe::getMainInstance();
        if ($probe->getResponseLine()) {
            $options['blackfire'] = true;
        }

        $response = $guzzle->request('GET', $url, $options);

You can find more information about :ref:`profiling HTTP requests
<php-sdk-http-profiling>` with the PHP SDK in the documentation.

Generating Builds Programmatically
----------------------------------

Creating builds via the SDK is another very powerful feature, which looks like
this:

.. code-block:: php

    // create a build
    $build = $blackfire->startBuild('example_env', array('title' => 'Build from PHP'));

    // create a scenario
    $scenario = $blackfire->startScenario($build, array('title' => 'My first scenario'));

    // add some profiles to the scenario, see below

    // end the scenario and fetch the report
    $report = $blackfire->closeScenario($scenario);

    // end the build
    $blackfire->closeBuild($build);

    // print the report URL
    print $report->getUrl();

Attaching profiles to a build can be done via the profile configuration:

.. code-block:: php

    // create a configuration
    $config = new \Blackfire\Profile\Configuration();

    // attach the scenario
    $config->setScenario($scenario);

How do you generate profiles now? There are so many ways that it is up to you!

Use the SDK to generate profiles for the current executed code:

.. code-block:: php

    // generate a profile via the SDK
    $probe = $blackfire->createProbe($config);

    // some PHP code you want to profile

    $blackfire->endProbe($probe);

    // generate some other profiles if that makes sense

Or use Guzzle for HTTP requests:

.. code-block:: php

    // generate a profile with Guzzle
    $response = $guzzle->request('GET', $url, array(
        'blackfire' => $config,
    ));

Conclusion
----------

Blackfire exposes a lot of features through the PHP SDK. This chapter showed
you various ways to use the SDK to solve advanced use cases.

The next logical step for the last recipe would be to generate dynamic
scenarios and store the results in build, taking flexibility to the next level.
This is a great topic for the next chapter.
