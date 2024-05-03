Guzzle [language: PHP]
======================

`Guzzle <http://docs.guzzlephp.org/>`_ is a PHP HTTP client that sends HTTP
requests and integrates well with web services. Integrating Blackfire with
Guzzle lets you **profile programmatically** your websites, HTTP APIs, or
web services.

Installation
------------

Add :ref:`Blackfire PHP SDK <php-sdk-installation>` as a dependency on your
project (1.21+ version).

.. caution::

    This document assumes Guzzle **version 6+**.

Profiling
---------

The Blackfire PHP SDK provides a **Guzzle middleware** that eases the profiling
of requests made via Guzzle:

.. code-block:: php
    :emphasize-lines: 6,13

    use GuzzleHttp\Client as GuzzleClient;
    use Blackfire\Client as BlackfireClient;
    use Blackfire\ClientConfiguration;
    use Blackfire\Bridge\Guzzle\Middleware as BlackfireMiddleware;

    $blackfire = new BlackfireClient(new ClientConfiguration($clientId, $clientToken));

    $guzzle = new GuzzleClient([
        // useful if you want to simulate a user experience
        'cookies' => true,
    ]);

    $guzzle->getConfig('handler')->push(BlackfireMiddleware::create($blackfire), 'blackfire');

Whenever you want to profile a request, set the ``blackfire`` option to
``true``:

.. code-block:: php
    :emphasize-lines: 12,16

    use Blackfire\Client as BlackfireClient;
    use Blackfire\ClientConfiguration;
    use GuzzleHttp\Client as GuzzleClient;
    use Blackfire\Bridge\Guzzle\Middleware as BlackfireMiddleware;

    $blackfire = new BlackfireClient(new ClientConfiguration($clientId, $clientToken));

    $guzzle = new GuzzleClient(['cookies' => true]);
    $guzzle->getConfig('handler')->push(BlackfireMiddleware::create($blackfire), 'blackfire');

    $response = $guzzle->request('GET', 'https://www.symfony.com/blog/', array(
        'blackfire' => true
    ));

    // get the profile for the request
    $profile = $blackfire->getProfile($response->getHeader('X-Blackfire-Profile-Uuid')[0]);

If you execute this script, a profile will be created on your Blackfire account
and tests defined in your ``.blackfire.yaml`` if any will be executed as well.
Note that the profile UUID is stored in the ``X-Blackfire-Profile-Uuid``
response header by the Blackfire middleware.

If you want to better control the profile configuration, like the title of the profile, pass a
``\Blackfire\Profile\Configuration`` instance as the ``blackfire`` option value:

.. code-block:: php
    :emphasize-lines: 2,3,6

    $config = new \Blackfire\Profile\Configuration();
    $config->setTitle('Blog Home');

    $response = $client->request('GET', 'https://www.symfony.com/blog/', array(
        'blackfire' => $config,
    ));

Learn more about :ref:`profiling configuration settings
<php-sdk-profile-configuration>` in the PHP SDK documentation.

.. _guzzle-builds:

Builds [level: Production]
--------------------------

As Guzzle provides great support for HTTP, you can create almost any HTTP
request you can think of, but more importantly, you can **simulate complex user
interactions**. Writing scenarios with Guzzle is a powerful alternative to the
:doc:`scenarios </builds-cookbooks/scenarios>` defined in a ``.blackfire.yaml`` file.

To generate a report from a scenario created with Guzzle, :ref:`store all
profiles in a build <php-sdk-builds>`:

.. code-block:: php
    :emphasize-lines: 2,5,20

    // create a build
    $build = $blackfire->startBuild('Symfony Prod', array('title' => 'Build from Guzzle'));

    // create a scenario
    $scenario = $blackfire->startScenario($build, array('title' => 'My first scenario'));

    // create a configuration
    $config = new \Blackfire\Profile\Configuration();
    $config->setScenario($scenario);

    // set the Profile and Job name
    $config->setTitle('Blog Home');

    // make a profiled request
    $client->request('GET', 'https://www.symfony.com/blog/', array(
        'blackfire' => $config
    ));

    // get the profile for the request
    $profile = $blackfire->getProfile($response->getHeader('X-Blackfire-Profile-Uuid')[0]);

    // end the scenario and fetch the report
    // the scenario contains one profile
    $report = $blackfire->closeScenario($scenario);

    // end the build
    $blackfire->closeBuild($build);

Note how we set the scenario on the configuration passed Guzzle.
