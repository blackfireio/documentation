Laravel Tests [level: Production]
=================================

Trigger Blackfire Builds with Laravel Tests
-------------------------------------------

Laravel provides a `framework for functional tests
<https://symfony.com/doc/current/testing.html#functional-tests>`_, working with
PHPUnit.

If you already implemented such tests, you may want to re-use them for your
performance tests using :doc:`Blackfire Builds </builds-cookbooks/index>`, and
avoid to write your test scenarios twice.

Using the Blackfire SDK, you can leverage these functional tests in order
to create :doc:`Blackfire Builds </builds-cookbooks/index>`, directly from your
CI system.

It relies on `Symfony HTTP Client <https://github.com/symfony/http-client>`_
in order to send real HTTP requests in the `testing` environment for the
profiled URLs.


Requirements
------------

- PHP >= 7.3
- Laravel >= 8.x
- PHPUnit >= 9.3

Installation
------------

Add :ref:`Blackfire PHP SDK <php-sdk-installation>` as a dependency in your
project (1.29+ version), together with Symfony HTTP Client.

.. code-block:: bash
    :zerocopy:

    composer require blackfire/php-sdk symfony/http-client

Edit your ``phpunit.xml.dist``:

.. code-block:: xml
    :emphasize-lines: 4-9

    <!-- phpunit.xml.dist -->
        <extensions>
            <!-- Blackfire extension -->
            <extension class="\Blackfire\Bridge\PhpUnit\Laravel\BlackfireBuildExtension">
                <arguments>
                    <string><!-- Your environment name or UUID --></string>
                    <string><!-- Name for the build (optional) --></string>
                </arguments>
            </extension>
        </extensions>

Create a ``env.testing`` file at the root of your Laravel application:

.. code-block:: ini

    APP_ENV=testing


Edit your ``app/Http/Kernel.php``:

.. code-block:: php
    :emphasize-lines: 5,9,14

    <?php

    ...

    use Blackfire\Bridge\Laravel\BlackfireTestHttpRequestsTrait;

    class Kernel extends HttpKernel
    {
        use BlackfireTestHttpRequestsTrait;

        protected $middleware = [
            // ...

            \Blackfire\Bridge\Laravel\InstrumentedTestRequests::class,
        ];

        // ...



Edit your ``app/Console/Kernel.php``:

.. code-block:: php
    :emphasize-lines: 5,9

    <?php

    // ...

    use Blackfire\Bridge\Laravel\BlackfireTestArtisanCommandsTrait;

    class Kernel extends ConsoleKernel
    {
        use BlackfireTestArtisanCommandsTrait;

        // ...


Usage
-----

In order to use your functional tests with Blackfire, you need to extend
the ``BlackfireTestCase``.

.. code-block:: php
    :emphasize-lines: 3,5

    namespace Tests\Feature;

    use Blackfire\Bridge\Laravel\BlackfireTestCase;

    class FooTest extends BlackfireTestCase
    {
        // Give a title to the scenario.
        protected $blackfireScenarioTitle = 'Name of this scenario';

        public function test_get(): void
        {
            $response = $this->get('/foo');

            $response->assertStatus(200);
        }
    }

.. note::

    A scenario is created for each instance of ``BlackfireTestCase``, each
    request being sent constituting a step of the scenario.

    You can specify the title for the ongoing scenario by setting the
    ``$blackfireScenarioTitle`` protected variable within your test case, like
    in the example above.

Temporarily Disable Profiling
-----------------------------

By default, every requests executed/tested within the test case` are profiled.

You may want to temporarily disable the profiling process for a few requests.
This is possible using the ``disableProfiling()`` method:

.. code-block:: php
    :emphasize-lines: 13

    namespace Tests\Feature;

    use Blackfire\Bridge\Laravel\BlackfireTestCase;

    class FooTest extends BlackfireTestCase
    {
        // Give a title to the scenario.
        protected $blackfireScenarioTitle = 'Name of this scenario';

        public function test_get(): void
        {
            $response = $this
                ->disableProfiling()
                ->get('/foo');

            $response->assertStatus(200);
        }
    }

Enable Profiling on selected Requests
-------------------------------------

You may want to enable the profiling process only for selected requests.
This is possible by disabling the automatic profiling of all requests and by
using the ``enableProfiling()`` method:

.. code-block:: php
    :emphasize-lines: 8,16

    namespace Tests\Feature;

    use Blackfire\Bridge\Laravel\BlackfireTestCase;

    class FooTest extends BlackfireTestCase
    {
        // Disable the automatic profiling of all requests
        protected $profileAllRequests = false;

        // Give a title to the scenario.
        protected $blackfireScenarioTitle = 'Name of this scenario';

        public function test_get(): void
        {
            $response = $this
                ->enableProfiling()
                ->get('/foo');

            $response->assertStatus(200);
        }
    }

Naming the Profiles
-------------------

The title of a profile triggered from the tests will be based on the URL and the
request's method. This title can be manually defined using the
``setProfileTitle`` method.

.. code-block:: php
    :emphasize-lines: 13

    namespace Tests\Feature;

    use Blackfire\Bridge\Laravel\BlackfireTestCase;

    class FooTest extends BlackfireTestCase
    {
        // Give a title to the scenario.
        protected $blackfireScenarioTitle = 'Name of this scenario';

        public function test_get(): void
        {
            $response = $this
                ->setProfileTitle('This Profile has a name')
                ->get('/foo');

            $response->assertStatus(200);
        }
    }


Test Artisan Commands
---------------------

Artisan Commands can be profiled as well using the ``BlackfireTestCase``.

.. note::

    The profiles of CLI commands cannot be included within the build. The
    profile URL will be printed if the shell output.

.. code-block:: php
    :emphasize-lines: 13

    namespace Tests\Feature;

    use Blackfire\Bridge\Laravel\BlackfireTestCase;

    class FooTest extends BlackfireTestCase
    {
        // Give a title to the scenario.
        protected $blackfireScenarioTitle = 'Name of this scenario';

        public function test_command(): void
        {
            $this
                ->artisan('list')
                ->assertExitCode(0);
            ;
        }
    }

Builds Comparison
-----------------

In order to :ref:`compare the current build to another one <assertions-comparisons>`,
you may set ``BLACKFIRE_EXTERNAL_ID`` and ``BLACKFIRE_EXTERNAL_PARENT_ID``
environment variables when launching your tests:

.. code-block:: bash

    BLACKFIRE_EXTERNAL_ID=current_build_reference \
    BLACKFIRE_EXTERNAL_PARENT_ID=parent_build_reference \
    php artisan test

.. note::

    You may use Git commit identifiers as references.

Globally Disable the Blackfire Build
------------------------------------

You may want to run Blackfire tests in a separate job in your pipeline, while
still running your functional tests.

In this case, it is possible to globally disable the Blackfire build by setting
the ``BLACKFIRE_BUILD_DISABLED`` environment variable to ``1``:

.. code-block:: bash

    BLACKFIRE_BUILD_DISABLED=1 php artisan test

.. note::

    Doing so also disables profiling for every HTTP requests.
