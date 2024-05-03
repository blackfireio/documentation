Goutte [language: PHP]
======================

`Goutte <https://github.com/FriendsOfPHP/goutte>`_ is a screen scraping and web
crawling library for PHP. Integrating Blackfire with Goutte lets you **profile
programmatically** your websites, HTTP APIs, or web services.

Installation
------------

First, add :ref:`Blackfire PHP SDK <php-sdk-installation>` as a dependency on
your project and be sure to require Goutte as well:

.. code-block:: bash

    composer require fabpot/goutte

Profiling
---------

To profile with Goutte, add the ``X-Blackfire-Query`` HTTP header before doing
any HTTP request you want to profile with Blackfire:

.. code-block:: php
    :emphasize-lines: 9,15

    use Goutte\Client as GoutteClient;
    use Blackfire\Client as BlackfireClient;

    $blackfire = new BlackfireClient();

    $client = new GoutteClient();

    // as we want to profile the next request, add the Blackfire header
    $profileRequest = $blackfire->createRequest('Blog Home');
    $client->setHeader('X-Blackfire-Query', $profileRequest->getToken());

    $crawler = $client->request('GET', 'https://www.symfony.com/blog/');

    // get the profile for the request
    $profile = $blackfire->getProfile($profileRequest->getUuid());

    $link = $crawler->selectLink('Security Advisories')->link();

    // also works before clicking on a link or submitting a form
    $client->setHeader('X-Blackfire-Query', $blackfire->createRequest('Security Advisories')->getToken());
    $crawler = $client->click($link);

.. caution::

    Never re-use a token for different HTTP requests.

If you execute this script, two profiles will be created on your Blackfire
account (tests defined in ``.blackfire.yaml`` will be executed as well if any).

Learn more about :ref:`profiling configuration settings
<php-sdk-profile-configuration>` in the PHP SDK documentation.

.. _goutte-builds:

Builds [level: Production]
--------------------------

As Goutte provides great support for HTTP, you can create almost any HTTP
request you can think of, but more importantly, you can **simulate complex user
interactions**. Writing scenarios with Goutte is a powerful alternative to the
:doc:`scenarios </builds-cookbooks/scenarios>` defined in a ``.blackfire.yaml`` file.

To generate a report from a scenario created with Goutte, :ref:`store all
profiles in a build <php-sdk-builds>`:

.. code-block:: php
    :emphasize-lines: 9,13,34

    use Goutte\Client as GoutteClient;
    use Blackfire\Client as BlackfireClient;

    $client = new GoutteClient();

    $blackfire = new BlackfireClient();

    // create a build
    $build = $blackfire->startBuild('Symfony Prod', array('title' => 'Build from Goutte'));

    // create a scenario
    $scenario = $blackfire->startScenario($build, array('title' => 'My first scenario'));

    // create a configuration
    $config = new \Blackfire\Profile\Configuration();
    $config->setScenario($scenario);

    // set the Profile and Job name
    $config->setTitle('Blog Home');

    // make a profiled request
    $profileRequest = $blackfire->createRequest($config);
    $client->setHeader('X-Blackfire-Query', $profileRequest->getToken());
    $crawler = $client->request('GET', 'https://www.symfony.com/blog/');

    // get the profile for the request
    $profile = $blackfire->getProfile($profileRequest->getUuid());

    // click on a link, generate another profile in the build
    $link = $crawler->selectLink('Security Advisories')->link();
    $config->setTitle('Security Advisories');
    $client->setHeader('X-Blackfire-Query', $blackfire->createRequest($config)->getToken());
    $crawler = $client->click($link);

    // end the scenario and fetch the report
    // the scenario contains two profiles
    $report = $blackfire->closeScenario($scenario);

    // end the build
    $blackfire->closeBuild($build);

Note that ``createRequest()`` received a ``Configuration`` tied to the scenario.
