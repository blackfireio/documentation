Symfony HTTPClient [language: PHP]
==================================

Symfony `HttpClient <https://symfony.com/doc/current/components/http_client.html>`_
is a PHP HTTP client that sends HTTP requests and integrates well with web services.
Integrating Blackfire with Symfony HttpClient lets you **profile programmatically**
your websites, HTTP APIs, or web services.

.. note::

    :ref:`Distributed Profiling <distributed-profiling>` allows you to trigger
    sub-profiles automatically, without having to trigger profiles programmatically.

Installation
------------

Add :ref:`Blackfire PHP SDK <php-sdk-installation>` as a dependency in
your project (1.19.1+ version).

Profiling
---------

The Blackfire PHP SDK provides a **Symfony HttpClient decorator** that eases the profiling
of requests made via HttpClient:

.. code-block:: php
    :emphasize-lines: 6,8

    use Blackfire\Bridge\Symfony\BlackfiredHttpClient;
    use Blackfire\Client;
    use Blackfire\ClientConfiguration;
    use Symfony\Component\HttpClient\HttpClient;

    $blackfire = new BlackfireClient(new ClientConfiguration($clientId, $clientToken));

    $httpClient = new BlackfiredHttpClient(HttpClient::create(), $blackfire);

Whenever you want to profile a request, set the ``blackfire`` extra option to
``true``:

.. code-block:: php

    $response = $httpClient->request('GET', 'https://www.symfony.com/blog/', [
        'extra' => [
            'blackfire' => true,
        ],
    ]);

If you execute this script, a profile will be created on your Blackfire account
and tests defined in your ``.blackfire.yaml`` if any will be executed as well.

If you want to better control the profile configuration, like the number of
samples or the title of the profile, pass a
``\Blackfire\Profile\Configuration`` instance as the ``blackfire`` extra option value:

.. code-block:: php
    :emphasize-lines: 2,3,6

    $config = new \Blackfire\Profile\Configuration();
    $config->setSamples(10);
    $config->setTitle('Blog Home');

    $response = $httpClient->request('GET', 'https://www.symfony.com/blog/', [
        'extra' => [
            'blackfire' => $config,
        ],
    ]);

When running this script, you will get one profile which will be the
aggregation of the 10 HTTP requests executed.

Learn more about :ref:`profiling configuration settings
<php-sdk-profile-configuration>` in the PHP SDK documentation.
