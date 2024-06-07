PHP SDK [language: PHP]
=======================

.. _php-sdk-installation:

Installation
------------

The Blackfire PHP SDK can be added as a requirement to your project via
`Composer <https://getcomposer.org/>`_:

.. code-block:: bash

    composer require blackfire/php-sdk

.. note::

    The PHP SDK works with PHP 5.3+.

.. tip::

    The Blackfire PHP SDK uses the same underlying mechanisms as the
    Blackfire CLI or the Blackfire Browser Extensions; so you need to
    :ref:`install <installation-instructions>` the Blackfire PHP extension and
    configure the Blackfire agent properly.

.. _php-blackfireprobe-internal-class:

The BlackfireProbe Internal Class
---------------------------------

The Blackfire probe exposes a class, which is part of the C extension, in the
root namespace: ``\BlackfireProbe``.

This class gives you the possibility to:

* Check if the probe is enabled;

* :ref:`Control the instrumentation <php-sdk-manual-instrumentation>`;

* :ref:`Add timeline markers <timeline-markers>`;

* :ref:`Generate sub-profiles <sub-profiles-php>`;

* :ref:`Name Monitoring Transactions programmatically <monitoring_naming_transactions_programmatically>`.

* :ref:`Ignore Monitoring Transactions <monitoring_ignoring_transactions>`.

.. code-block:: php

    final class BlackfireProbe
    {
        /**
         * Returns a global singleton of the probe.
         *
         * @return \BlackfireProbe
         */
        public static function getMainInstance() {}

        /**
         * Tells whether the probe is currently profiling or not.
         *
         * @return bool
         */
        public static function isEnabled() {}

        /**
         * Adds a marker for the Timeline View.
         * Production safe. Operates a no-op if no profile is requested.
         *
         * @param string $markerName
         */
        public static function addMarker($markerName = '') {}

        /**
         * Tells if the probe is cryptographically verified,
         * i.e. if the signature in X-Blackfire-Query HTTP header or
         * BLACKFIRE_QUERY environment variable is valid.
         *
         * @return bool
         */
        public function isVerified() {}

        /**
         * Enables manual instrumentation. Starts collecting profiling data.
         * Production safe. Operates a no-op if no profile is requested.
         *
         * @return bool False if enabling failed.
         */
        public function enable() {}

        /**
         * Discards collected data and disables instrumentation.
         *
         * Does not close the profile payload, allowing to re-enable the probe and aggregate data in the same profile.
         *
         * @return bool False if the probe was not enabled.
         */
        public function discard() {}

        /**
         * Disables instrumentation.
         * Production safe. Operates a no-op if no profile is requested.
         *
         * Does not close the profile payload, allowing to re-enable the probe
         * and to aggregate data in the same profile.
         *
         * @return bool False if the probe was not enabled.
         */
        public function disable() {}

        /**
         * Stops the profiling and forces the collected data to be sent to Blackfire.
         *
         * @return bool False if the probe was not enabled.
         */
        public function close() {}

        /**
         * Creates a sub-query string to create a new profile linked to the current one.
         * Generated query must be set in the X-Blackfire-Query HTTP header or in the BLACKFIRE_QUERY environment variable.
         *
         * @return string|null The sub-query or null if profiling is disabled.
         */
        public function createSubProfileQuery() {}

        /**
         * Sets a custom transaction name for Blackfire Monitoring.
         */
        public function setTransactionName() {}

        /**
         * Disables Blackfire Monitoring instrumentation for a transaction.
         */
        public function ignoreTransaction() {}       
    }

Blackfire PHP SDK
-----------------

The **Blackfire PHP SDK** allows you to generate profiles from your code and
it eases the integration with third-party libraries (like :doc:`PHPUnit
</php/integrations/phpunit>`). It can also be used to :ref:`profile HTTP
requests from PHP <php-sdk-http-profiling>`.

The main entry point of the SDK is the ``Blackfire\Client`` class:

.. code-block:: php

    $blackfire = new \Blackfire\Client();

Profiling
~~~~~~~~~

The client object allows you to profile any parts of your code:

.. code-block:: php

    $probe = $blackfire->createProbe();

    // some PHP code you want to profile

    $profile = $blackfire->endProbe($probe);

The ``createProbe()`` method takes an optional
``Blackfire\Profile\Configuration`` object that allows you to :ref:`configure
the Blackfire Profile <php-sdk-profile-configuration>` more finely:

.. code-block:: php

    $config = new \Blackfire\Profile\Configuration();
    $probe = $blackfire->createProbe($config);

When calling ``endProbe()``, the profile is generated and sent to Blackfire.io
servers. The ``$profile`` variable is an instance of ``Blackfire\Profile``
that gives you access to the generated :ref:`profile information
<php-sdk-profile>`.

You can store the profile UUID to get it back later:

.. code-block:: php

    // store the profile UUID
    $uuid = $probe->getRequest()->getUuid();

    // retrieve the profile later on
    $profile = $blackfire->getProfile($uuid);

The ``$probe`` instance can also be used to instrument precisely only part of
your code:

.. code-block:: php

    $blackfire = new \Blackfire\Client();

    // false here means that we want to instrument the code ourselves
    $probe = $blackfire->createProbe(null, false);

    // some code that won't be instrumented

    // start instrumentation and profiling
    $probe->enable();

    // some code that is going to be profiled

    // stop instrumentation
    $probe->disable();

    // code here won't be profiled

    // do it as many times as you want
    // all profiled sections will be aggregated in one graph
    $probe->enable();
    $probe->disable();

    // end the profiling session
    $profile = $blackfire->endProbe($probe);

Note that having many ``enable()/disable()`` sections might make your call
graph very difficult to interpret. You might want to create several profiles
instead.

.. tip::

    Enabling the instrumentation via the Probe object instead of the Client one
    is very useful when you integrate Blackfire deeply in your code. For
    instance, you might create the Blackfire Client in one object and do the
    profiling in another portion of your code.

.. _php-sdk-profile:

Profile
~~~~~~~

``Blackfire\Profile`` instances (as returned by ``Client::endProbe()``)
give you access to generated profiles data:

.. code-block:: php

    $profile = $blackfire->endProbe($probe);

You can also get any profile by UUID:

.. code-block:: php

    $profile = $blackfire->getProfile($uuid);

Here is a quick summary of available methods:

.. code-block:: php

    // the profile URL
    $profile->getUrl();

    // get the main costs
    $cost = $profile->getMainCost();

    // get SQL queries (returns an array of Cost instances)
    $queries = $profile->getSqls();

    // get HTTP requests (returns an array of Cost instances)
    $requests = $profile->getHttpRequests();

    // Cost methods
    $cost->getWallTime();
    $cost->getCpu();
    $cost->getIo();
    $cost->getNetwork();
    $cost->getPeakMemoryUsage();
    $cost->getMemoryUsage();

You can also access the Blackfire test results:

.. code-block:: php

    // tests were successful (all assertions pass)
    $profile->isSuccessful();

    // an error occurred when running the tests (different from assertion failures)
    // an error can be a syntax error in an assertion for instance
    $profile->isErrored();

    // get test results (returns an array of Blackfire\Profile\Test instances)
    $tests = $profile->getTests();

    // display all failures
    if (!$profile->isErrored()) {
        foreach ($tests as $test) {
            if ($test->isSuccessful()) {
                continue;
            }

            printf("    %s: %s\n", $test->getState(), $test->getName());

            foreach ($test->getFailures() as $assertion) {
                printf("      - %s\n", $assertion);
            }
        }
    }

.. _php-sdk-profile-configuration:

Profile Basic Configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~

The ``Client::createProbe()`` method takes a
``Blackfire\Profile\Configuration`` instance that allows to configure profile
generation:

.. code-block:: php

    $config = new \Blackfire\Profile\Configuration();
    $probe = $blackfire->createProbe($config);

    // set the profile title
    $config->setTitle('Homepage');

    // attach some metadata to the profile
    $config->setMetadata('pull-request', 42);

    // By default, profiles created with the SDK won't appear in the profiles list.
    // Disable "skip_timeline" if you want your profiles to be listed anyway.
    // "false" must be passed as a string. "0" is valid as well.
    //$config->setMetadata('skip_timeline', 'false');

.. tip::

    The Configuration class implements a fluent interface:

    .. code-block:: php

        $config = (new \Blackfire\Profile\Configuration())->setTitle('Homepage')->setMetadata('pull-request', 42);

.. _php-sdk-assertions-configuration:

Profile Assertions Configuration [level: Development/Production]
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Besides basic profile configuration, you can also configure :doc:`assertions
</testing-cookbooks/assertions>`:

.. code-block:: php

    // set some assertions
    // first argument is the assertion, second one is the assertion/test name
    $config->assert('metrics.sql.queries.count > 50', 'I want many SQL requests');

.. note::

    To keep the API simple and unlike tests defined in ``.blackfire.yaml``,
    tests defined via ``assert()`` only ever contains one assertion.

.. _php-sdk-custom-metrics:

If you need to, you can create some custom metrics as well:

.. code-block:: php

    use Blackfire\Profile\Metric;

    // define a custom metric
    $metric = new Metric('cache.write_calls', '=Cache::write');

    // add it to the profile configuration
    // to  be able to use it in assertions
    $config->defineMetric($metric);

When defining a ``Metric``, the first constructor argument is the metric name
(``cache.write_calls`` here) which can used in an assertion by prefixing it
with ``metrics.`` and appending a dimension (like in
``metrics.cache.write_calls.count``).

The second constructor argument is a :ref:`method selector <metrics-selectors>`
or an array of method selectors:

    .. code-block:: php

        $metric = new Metric('cache.write_calls', array('=Cache::write', '=Cache::store'));

.. _php-sdk-http-profiling:

HTTP Profiling
~~~~~~~~~~~~~~

Using the Blackfire Client, you can create HTTP scenarios directly from PHP.
Enabling code instrumentation for HTTP requests is done via a specific HTTP
header (``X-Blackfire-Query``); the value containing the profile configuration
and a signature used for authorization.

.. code-block:: php

    $blackfire = new \Blackfire\Client();

    // generate the HTTP header to enable Blackfire
    $request = $blackfire->createRequest();
    $header = 'X-Blackfire-Query: '.$request->getToken();

Specify the profile title via the first argument:

.. code-block:: php

    $request = $blackfire->createRequest('Homepage');

Or pass a full ``Blackfire\Profile\Configuration`` instance:

.. code-block:: php

    $config = (new \Blackfire\Profile\Configuration())->setTitle('Homepage');
    $request = $blackfire->createRequest($config);

Get the generated profile from the profile request:

.. code-block:: php

    $profile = $blackfire->getProfile($request->getUuid());

Learn more about how to use this feature with :doc:`Guzzle
</php/integrations/guzzle>` or :doc:`Goutte </php/integrations/goutte>`.

Error Management
~~~~~~~~~~~~~~~~

When an error occurs because of Blackfire, a
``\Blackfire\Exception\ExceptionInterface`` exception instance is thrown:

* ``\Blackfire\Exception\NotAvailableException``: The Blackfire PHP extension
  is not installed or not enabled.

* ``\Blackfire\Exception\OfflineException``: You are offline or the Blackfire
  servers are not reachable (check your proxy configuration).

* ``\Blackfire\Exception\ApiException``: An error occurred when communicating
  with Blackfire.

* ``\Blackfire\Exception\ConfigNotFoundException``: The Blackfire configuration
  file cannot be found.

* ``\Blackfire\Exception\EnvNotFoundException``: The configured environment
  does not exist.

To avoid breaking your code when such errors occur, wrap your code and catch
the interface:

.. code-block:: php

    try {
        $probe = $blackfire->createProbe($config);

        // do something

        $profile = $blackfire->endProbe($probe);
    } catch (\Blackfire\Exception\ExceptionInterface $e) {
        // Blackfire error occurred during profiling
        // do something
    }

Client Configuration
~~~~~~~~~~~~~~~~~~~~

When creating a Client, Blackfire uses your local Blackfire configuration by
default (stored in ``~/.blackfire.ini``). But you can also set the configuration
explicitly:

.. code-block:: php

    // all arguments are optional
    $config = new \Blackfire\ClientConfiguration($clientId, $clientToken, $defaultEnv);

    // or read it from a file
    $config = \Blackfire\ClientConfiguration::createFromFile('some-blackfire.ini');

    // use the configuration
    $blackfire = new \Blackfire\Client($config);

By default, profiles are sent to your personal profiles, but you can change the
**environment** via the ``setEnv()`` method:

.. code-block:: php

    $config->setEnv('mywebsite');

.. _php-sdk-builds:

Scenarios & Builds [level: Production]
--------------------------------------

.. note::

    Instead of creating Scenarios and Builds programmatically like described below,
    you may **consider one of the following integrations** provided by the PHP SDK:

    - :doc:`Symfony Functional Tests </php/integrations/symfony/functional-tests>`

    - :doc:`Behat </php/integrations/behat>`

When generating more than one profile, like when you profile **complex user
interactions** with your application, you might want to aggregate them in a
scenario.
Scenarios can be grouped in a build.

Using builds and scenarios has the following benefits:

* A scenario written in PHP is a powerful alternative to the :doc:`scenarios
  </builds-cookbooks/scenarios>` defined in a ``.blackfire.yaml`` file.

* A scenario consolidates tests results and generates a :ref:`Report <build-report>`

* A build consolidates **scenarios results** and **sends notifications**
  (GitHub, Slack, ...);

* A build contains **all profiles from a profiling session** (individual profiles
  are not displayed in the dashboard anymore);

Creating a scenario is not that different from profiling individual pages as
described in the previous paragraphs:

.. code-block:: php
    :emphasize-lines: 2,9,19

    // create a build (optional)
    $build = $blackfire->startBuild('Symfony Prod', array(
        'title' => 'Build from PHP',
        'trigger_name' => 'PHP',
    ));

    // create a scenario (if the $build argument is null, a new build will be created)
    $scenario = $blackfire->startScenario($build, array(
        'title' => 'Test documentation'
    ));

    // create a configuration
    $config = new \Blackfire\Profile\Configuration();
    $config->setScenario($scenario);

    // create as many profiles as you need
    $probe = $blackfire->createProbe($config);

    // some PHP code you want to profile

    $blackfire->endProbe($probe);

    // end the scenario and fetch the report
    $report = $blackfire->closeScenario($scenario);

    // end the build
    $blackfire->closeBuild($build);
    // or if the build was created automatically: $blackfire->closeBuild($scenario->getBuild());

To create a build, call ``startBuild()`` and pass it the environment name (or
UUID). Optionally pass an array of options:

* ``title``: A build title;

* ``trigger_name``: A trigger name (displayed in the dashboard);

* ``external_id``: A unique identifier for the build; commonly, a unique
  reference from a third party service like the Git commit sha1 related to the
  build. It is used by some notifications (like GitHub);

* ``external_parent_id``: The unique identifier of the parent build.

.. tip::

    The ``external_id`` and ``external_parent_id`` options can be used to
    :doc:`integrate Blackfire with GitHub pull request statuses </integrations/git/github>`

To create a scenario, call ``startScenario()`` and pass it a build,
or null to create a new build). Optionally pass an array of options:

* ``title``: A scenario title;

* ``metadata``: An array of metadata to associated with the scenario;

* ``external_id``: A unique identifier for the scenario;

* ``external_parent_id``: The unique identifier of the parent scenario.
  It is used to compare scenarios;

To store a profile in the scenario, call ``createProbe()`` and pass it a
``Configuration`` object that has been tied to the scenario
(``$config->setScenario($scenario)``).

Stop the scenario by calling ``closeScenario()`` and the build by calling ``closeBuild()``.
The ``closeScenario()`` call returns the :ref:`Report <php-sdk-report>` when ready.

You can store the scenario UUID to get report back later:

.. code-block:: php

    // store the scenario UUID
    $uuid = $scenario->getUuid();

    // retrieve the report later on
    $report = $blackfire->getReport($uuid);

.. tip::

    HTTP scenarios can be created with :ref:`Goutte <goutte-builds>` or
    :ref:`Guzzle <guzzle-builds>`.

.. _php-sdk-report:

Report
~~~~~~

``Blackfire\\Report`` instances (as returned by ``Client::closeScenario()``) give
you access to builds data:

.. code-block:: php

    $report = $blackfire->closeScenario($scenario);

You can also get any report by UUID:

.. code-block:: php

    $report = $blackfire->getReport($uuid);

Here is a summary of available methods:

.. code-block:: php

    // the report URL
    $report->getUrl();

    // tests were successful (all assertions pass)
    $report->isSuccessful();

    // an error occurred when running the tests (different from assertion failures)
    // an error can be a syntax error in an assertion for instance
    $report->isErrored();

.. _php-sdk-manual-instrumentation:

Controlling Automatic Instrumentation
-------------------------------------

When using the Blackfire CLI or a browser, Blackfire automatically instruments
your code. If you want to control which part of the code is instrumented, you
need to enable and disable instrumentation manually.

You can manually instrument some code by using the ``\BlackfireProbe`` :ref:`class
that comes bundled with the Blackfire's probe <php-blackfireprobe-internal-class>`:

.. code-block:: php

    // Get the probe main instance
    $probe = BlackfireProbe::getMainInstance();

Starts gathering profiling data by calling ``enable()``:

.. code-block:: php

    // start profiling the code
    $probe->enable();

Stops the profiling by calling ``disable()``:

.. code-block:: php

    // stop the profiling
    $probe->disable();

You can call ``enable()`` and ``disable()`` as many times as needed in your
code. You can also discard any collected data by calling ``discard()``.

Calling ``close()`` instead of ``disable()`` stops the profiling and forces the
collected data to be sent to Blackfire:

.. code-block:: php

    // stop the profiling
    // send the result to Blackfire
    $probe->close();

.. caution::

    As with auto-instrumentation, profiling is only active when the code is run
    through the browser extension or the ``blackfire`` CLI utility. If not,
    **all calls are converted to no-ops**.

.. _php-sdk-profiling-consumers-daemons:

Profiling Consumers and Daemons
-------------------------------

The PHP SDK provides a way to profile consumers and daemons via the
``LoopClient`` class:

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
number of iterations for each profile. Call ``startLoop()`` when entering a new
loop iteration (before consuming a message for instance), and call
``endLoop()`` at the end of the message processing.

.. _php-sdk-signals:

Calling the ``generateBuilds()`` method automatically configures ``LoopClient``
to generate a build for each profile:

.. code-block:: php

    $blackfire->generateBuilds('ENV_NAME_OR_UUID');

If you need more flexibility, like setting a different title for each build,
pass a Build factory as the second argument:

.. code-block:: php

    use Blackfire\Client;

    $blackfire->generateBuilds('ENV_NAME_OR_UUID', function (Client $blackfire, $env) {
        return $blackfire->startBuild($env, array('title' => 'Some generated title'));
    });

Using Signals
~~~~~~~~~~~~~

Profiling a consumer continuously is never a good idea. Instead, you should
profile your consumers on demand or regularly.

``LoopClient`` supports this use case via signals. Register the signal you want
to use for profiling and the code will only profile when signaled:

.. code-block:: php

    $blackfire = new LoopClient(new Client(), 10);
    $blackfire->setSignal(SIGUSR1);

With this code in place, generating a profile of your consumer can be done by
sending the ``SIGUSR1`` signal to the process:

.. code-block:: bash

    pkill -SIGUSR1 -f consumer.php

Signal the consumer with ``SIGUSR1`` to generate a regular profile.

.. note::

    Triggering profiles on a pre-defined schedule can be done by adding an
    entry in the crontab that signals the consumer process.

.. _php-sdk-commit-status:

Enabling the Update of Git Commit Statuses
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When using the SDK to automatically run test scenarios on git branches, for
instance with a :doc:`GitHub integration </integrations/git/github>` or
:doc:`GitLab integration </integrations/git/gitlab>`, you will need to update
the commit status to ease the validation and merge decision.

Commit statuses are associated to builds via the corresponding Git commit sha1.
After enabling the :doc:`notification channel
</builds-cookbooks/notification-channels>` (GitHub, Gitlab, or webhooks) for an
environment, pass the Git sha1 to the ``startBuild()`` method options:

.. code-block:: php
    :emphasize-lines: 3

    $build = $blackfire->startBuild('env-name-or-uuid', array(
        'title' => 'Build from PHP',
        'external_id' => '178f05003a095eb6b3a838d403544962262b7ed4',
    ));

.. note::

    You must pass the full 40-character sha1 or GitHub won't accept the commit
    statuses.

To activate the comparison assertions on scenarios, pass a ``external_parent_id``
to the scenario's options.
This is typically the sha1 of the base branch of the pull request, concatenated
with the name of the scenario:

.. code-block:: php
    :emphasize-lines: 3-4

    $scenario = $blackfire->startScenario($build, array(
        'title' => 'My Scenario',
        'external_id' => '178f05003a095eb6b3a838d403544962262b7ed4:my-scenario',
        'external_parent_id' => 'f72aa774dd33cfc5eac43e1bfaf67e4028acca8b:my-scenario',
    ));

.. _sub-profiles-php:

Generating Sub-Profiles
-----------------------

Thanks to the :ref:`Distributed Profiling feature <distributed-profiling>`, you
can embed *sub-profiles* in the main profile.

For instance, when profiling an application that calls HTTP services and/or
sub-processes, you might want to trigger profiles for them as well. In PHP, the
process can be either automatic or manual, depending on what you need to do.

Distributed Profiling with HTTP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Blackfire PHP probe supports **automatic sub-profiles generation** when doing
HTTP requests with:

* ``cURL``;

* HTTP streams (``fopen``/``file_get_contents``).

These 2 methods cover most of the HTTP client libraries available for PHP,
including Symfony HttpClient, Guzzle, Goutte, etc.

If you use a different way to send HTTP requests, you then have to generate a
sub-profile query manually. This query must be added as an
``X-Blackfire-Query`` HTTP header.

This is for instance the case when using the SOAP extension for PHP:

.. code-block:: php

    $soapOpts = [];
    $probe = \BlackfireProbe::getMainInstance();
    if (\BlackfireProbe::isEnabled()) {
        $soapOpts += [
            'stream_context' => stream_context_create([
                'http' => [
                    'header' => 'X-Blackfire-Query: '.$probe->createSubProfileQuery(),
                ],
            ]),
        ];
    }

    $client = new \SoapClient('some.wsdl', $soapOpts);

Distributed Profiling with CLI
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

It is also possible to trigger sub-profiles when spawning CLI processes from
PHP scripts. The process is the same as for HTTP, except that the
sub-profile query must be assigned to the ``BLACKFIRE_QUERY`` environment
variable, which must be exposed to the CLI process.

.. code-block:: php

    // Spawning to sub.php.
    // Works with any language supported by Blackfire.

    $processEnv = $_ENV;
    if (\BlackfireProbe::isEnabled()) {
        $probe = \BlackfireProbe::getMainInstance();
        $processEnv['BLACKFIRE_QUERY'] = $probe->createSubProfileQuery();
    }

    $proc = proc_open(
        'php sub.php',
        [STDIN, STDOUT, STDOUT],
        $pipes, null,
        $processEnv
    );
    proc_close($proc);
