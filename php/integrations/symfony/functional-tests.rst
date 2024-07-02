Symfony Functional Tests [level: Production]
============================================

Trigger Blackfire Builds with Symfony Functional Tests
------------------------------------------------------

Symfony provides a `useful framework for functional tests
<https://symfony.com/doc/current/testing.html#functional-tests>`_, working with
PHPUnit.

If you already implemented such tests, you may want to re-use them for your
performance tests using :doc:`Blackfire Builds </builds-cookbooks/index>`, and
avoid to write your test scenarios twice.

Using the Blackfire SDK, you can leverage these functional tests in order
to create :doc:`Blackfire Builds </builds-cookbooks/index>`, directly from your
CI system.

It uses `Symfony Panther <https://github.com/symfony/panther>`_ in the background,
in order to send real HTTP requests, and to manage the PHP built-in webserver.

.. note::

    Despite the use of Symfony Panther, this integration does not use ChromeDriver
    nor GeckoDriver, and thus does not support JavaScript.

Requirements
------------

- PHP >= 7.1
- Symfony >= 4.x
- PHPUnit >= 8.x

Installation
------------

Add :ref:`Blackfire PHP SDK <php-sdk-installation>` as a dependency in
your project, together with Symfony Panther:

.. code-block:: bash
    :zerocopy:

    composer require blackfire/php-sdk symfony/panther

Edit your ``phpunit.xml.dist``:

.. code-block:: xml

    <!-- phpunit.xml.dist -->
        <extensions>
            <!-- Add Symfony Panther extension -->
            <extension class="Symfony\Component\Panther\ServerExtension" />
            <!-- Blackfire extension -->
            <extension class="\Blackfire\Bridge\PhpUnit\BlackfireBuildExtension">
                <arguments>
                    <string><!-- Your environment name or UUID --></string>
                    <string><!-- Name for the build (optional) --></string>
                </arguments>
            </extension>
        </extensions>

Usage
-----

In order to use your functional tests with Blackfire, you need to either extend
the ``BlackfireTestCase`` or import the ``BlackfireTestCaseTrait``.

Then, you can use the ``BlackfiredHttpBrowserClient`` instead of the Symfony
functional test client.

**Extending BlackfireTestCase**:

.. code-block:: php
    :emphasize-lines: 6,9,14

    namespace App\Tests\Controller;

    use App\Pagination\Paginator;
    use Blackfire\Bridge\PhpUnit\BlackfireTestCase;

    class BlogControllerTest extends BlackfireTestCase
    {
        // Give a title to the scenario.
        protected const BLACKFIRE_SCENARIO_TITLE = 'Blog Controller';

        public function testIndex(): void
        {
            // Create the Blackfire enabled HTTP browser.
            $client = static::createBlackfiredHttpBrowserClient();
            $crawler = $client->request('GET', '/en/blog/');

            $this->assertResponseIsSuccessful();

            $this->assertCount(
                Paginator::PAGE_SIZE,
                $crawler->filter('article.post'),
                'The homepage displays the right number of posts.'
            );
        }
    }

**Using BlackfireTestCaseTrait**:

.. code-block:: php
    :emphasize-lines: 4,9,12,17

    namespace App\Tests\Controller;

    use App\Pagination\Paginator;
    use Blackfire\Bridge\PhpUnit\BlackfireTestCaseTrait;
    use PHPUnit\Framework\TestCase;

    class BlogControllerTest extends TestCase
    {
        use BlackfireTestCaseTrait;

        // Give a title to the scenario.
        protected const BLACKFIRE_SCENARIO_TITLE = 'Blog Controller';

        public function testIndex(): void
        {
            // Create the Blackfire enabled HTTP browser.
            $client = static::createBlackfiredHttpBrowserClient();
            $crawler = $client->request('GET', '/en/blog/');

            $this->assertResponseIsSuccessful();

            $this->assertCount(
                Paginator::PAGE_SIZE,
                $crawler->filter('article.post'),
                'The homepage displays the right number of posts.'
            );
        }
    }

.. note::

    A scenario is created for each instance of ``BlackfireTestCase`` /
    ``BlackfireTestCaseTrait``, each request being sent constituting a step of
    the scenario.

    You can specify the title for the ongoing scenario by setting the
    ``BLACKFIRE_SCENARIO_TITLE`` class constant within your test case, like
    in the example above.

Behind the scenes, Panther automatically starts the PHP built-in server.
Please refer to `Panther documentation if you want to customize the webserver
<https://github.com/symfony/panther#environment-variables>`_.

.. note::

    A nice alternative to the PHP built-in server is the `Symfony Local Web Server
    <https://symfony.com/doc/current/setup/symfony_server.html>`_.

    To do this, you need to set the ``PANTHER_EXTERNAL_BASE_URI``
    environment variable with the complete base URI of Symfony server endpoint:

    .. code-block:: xml

        <!-- phpunit.xml.dist -->
            <php>
                <server name="PANTHER_EXTERNAL_BASE_URI" value="https://localhost:8000" force="true" />
            </php>

    You also need to ensure that it is running before launching the PHPUnit
    test suite.

.. _symfony-functional-tests-manual-scenarios:

Create Scenarios Manually
-------------------------

By default, a :doc:`scenario </builds-cookbooks/scenarios>` is created for each
instance of ``BlackfireTestCase`` and ``BlackfireTestCaseTrait``, each request
being sent constituting :doc:`a step of the scenario </builds-cookbooks/scenarios>`.

You may want to control this behavior and create the scenarios manually.
To do this, you need to define a ``BLACKFIRE_SCENARIO_AUTO_START`` class constant
in your test case, and set it to ``false``.

You can then use the ``BuildHelper`` to create and end your scenarios:

.. code-block:: php
    :emphasize-lines: 9,14,15,18,30

    namespace App\Tests\Controller;

    use App\Pagination\Paginator;
    use Blackfire\Bridge\PhpUnit\BlackfireTestCase;

    class BlogControllerTest extends BlackfireTestCase
    {
        // Disable Blackfire Scenario Auto-Start.
        protected const BLACKFIRE_SCENARIO_AUTO_START = false;

        public function testIndex(): void
        {
            // Create the scenario.
            $buildHelper = BuildHelper::getInstance();
            $buildHelper->createScenario('Title for my scenario');

            // Create the Blackfire enabled HTTP browser.
            $client = static::createBlackfiredHttpBrowserClient();
            $crawler = $client->request('GET', '/en/blog/');

            $this->assertResponseIsSuccessful();

            $this->assertCount(
                Paginator::PAGE_SIZE,
                $crawler->filter('article.post'),
                'The homepage displays the right number of posts.'
            );

            // Don't forget to end the scenario.
            $buildHelper->endCurrentScenario();
        }
    }

Temporarily Disable Profiling
-----------------------------

By default, every requests sent by the ``BlackfiredHttpBrowserClient`` are
profiled.

You may want to temporarily disable the profiling process for a few requests.
This is possible using the ``disableProfiling()`` method:

.. code-block:: php
    :emphasize-lines: 25,33

    namespace App\Tests\Controller;

    use App\Pagination\Paginator;
    use Blackfire\Bridge\PhpUnit\BlackfireTestCase;

    class BlogControllerTest extends BlackfireTestCase
    {
        // Give a title to the scenario.
        protected const BLACKFIRE_SCENARIO_TITLE = 'Blog Controller';

        public function testNewComment(): void
        {
            // Create the Blackfire enabled HTTP browser.
            $client = static::createBlackfiredHttpBrowserClient();
            $client->followRedirects();

            // Find first blog post
            $crawler = $client->request('GET', '/en/blog/');
            $postLink = $crawler->filter('article.post > h2 a')->link();

            $client->click($postLink);
            $client->clickLink('Sign in');

            // Temporarily disable profiling.
            $client->disableProfiling();

            $client->submitForm('Sign in', [
                '_username' => 'john_user',
                '_password' => 'kitten',
            ]);

            // Re-enable profiling.
            $client->enableProfiling();

            $crawler = $client->submitForm('Publish comment', [
                'comment[content]' => 'Hi, Symfony!',
            ]);

            $newComment = $crawler->filter('.post-comment')->first()->filter('div > p')->text();

            $this->assertSame('Hi, Symfony!', $newComment);
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
    bin/phpunit tests/Controller/BlogControllerTest

.. note::

    You may use Git commit identifiers as references.

Globally Disable the Blackfire Build
------------------------------------

You may want to run Blackfire tests in a separate job in your pipeline, while
still running your functional tests.

In this case, it is possible to globally disable the Blackfire build by setting
the ``BLACKFIRE_BUILD_DISABLED`` environment variable to ``1``:

.. code-block:: bash

    BLACKFIRE_BUILD_DISABLED=1 bin/phpunit tests/Controller/BlogControllerTest

.. note::

    Doing so also disables profiling for every HTTP requests sent by the
    ``BlackfiredHttpBrowser``.

Note about ``setUpBeforeClass()`` and ``tearDownAfterClass()``
--------------------------------------------------------------

The ``BlackfireTestCaseTrait`` leverages the ``setUpBeforeClass()`` and
``tearDownAfterClass()`` methods from the base PHPUnit ``TestCase`` class.

If you already use them within a test case that you want to use with Blackfire,
the scenario auto-start will not work, as the mentioned methods will be overridden
by the ones defined in your test case class.

In this case, you need to :ref:`create the scenarios manually
<symfony-functional-tests-manual-scenarios>`.
