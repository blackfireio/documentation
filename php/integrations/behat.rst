Behat [level: Production]
=========================

Trigger Blackfire Builds with Behat
-----------------------------------

`Behat <https://behat.org>`_ is a popular and open-source Behavior-Driven-Development
(aka BDD) framework for PHP.

It makes it possible to write tests using a structured natural language.
For testing applications in a web context, it uses another component, Mink,
which role is to manage *browser sessions* using drivers.

If you already implemented such tests, you may want to re-use them for your
performance tests using :doc:`Blackfire Builds </builds-cookbooks/index>`, and
avoid writing your test scenarios twice.

Using the Blackfire SDK, you can leverage these tests to create :doc:`Blackfire
Builds </builds-cookbooks/index>`, directly from your CI system.

Requirements
------------

- PHP >= 7.2
- Behat 3
- ``friends-of-behat/mink-extension`` >= 2.0
- ``friends-of-behat/mink-browserkit-driver`` >= 1.5
- ``friends-of-behat/symfony-extension`` >= 2.0 (Optional, only required if you want to use the Symfony driver)

.. note::

    Note that the original ``behat/mink-extension``, ``behat/symfony2-extension`` and ``minkphp/mink-browserkit-driver``
    will not work with the Blackfire extension.

Installation
------------

Add :ref:`Blackfire PHP SDK <php-sdk-installation>` as a dependency in
your project (1.25+ version), together with the Mink extension and the BrowserKit
driver:

.. code-block:: bash
    :zerocopy:

    composer require blackfire/php-sdk friends-of-behat/mink-extension friends-of-behat/mink-browserkit-driver

If you want to use the Symfony driver, also install the Symfony extension:

.. code-block:: bash
    :zerocopy:

    composer require friends-of-behat/symfony-extension

Usage
-----

Edit your Behat configuration file:

.. code-block:: yaml
    :emphasize-lines: 5,7,9,15

    # behat.yaml.dist
    default:
        extensions:
            # Declare and configure the BlackfireExtension
            Blackfire\Bridge\Behat\BlackfireExtension:
                # UUID or name of your Blackfire environment
                blackfire_environment: 'My Blackfire environment'
                # The name you want to give to your Blackfire Builds triggered by Behat
                build_name: 'BDD test with Behat'
            Behat\MinkExtension:
                base_url: 'https://localhost:8000'
                sessions:
                    default:
                        # Declare the Blackfire Mink driver
                        blackfire: ~

        suites:
            'Main Suite':
                contexts:
                    - FeatureContext
                    - Behat\MinkExtension\Context\MinkContext

Now, every time you launch the ``behat`` command, Mink is going to use the
Blackfire driver. Every step in your Behat scenario is going to be profiled
unless you tell it otherwise from a feature context.

If you use the above configuration, tests will be run using the Browserkit driver which performs actual requests
against your code. If you are using Symfony, you may prefer to use the kernel browser driver, which does not perform
actual requests, only simulates them by directly calling the Symfony kernel and which is much faster. In this case,
change the above configuration to:

.. code-block:: yaml
    :emphasize-lines: 6

    # behat.yaml.dist
                ...
                sessions:
                    default:
                        # Declare the Blackfire Symfony kernel browser driver
                        blackfire_symfony: ~


**A Blackfire Build is created for each defined Behat Suite**.
As such, every scenario defined in a suite is considered part of the corresponding
:doc:`Blackfire Build </builds-cookbooks/index>`.

**By default, every HTTP requests sent by the** ``blackfire`` **Mink driver
are profiled**.

However, you can control this behavior with the ``disableProfiling()`` and
``enableProfiling()`` functions from the ``BlackfireContextTrait``:

.. code-block:: php
    :emphasize-lines: 2,6,14,18

    use Behat\MinkExtension\Context\RawMinkContext;
    use Blackfire\Bridge\Behat\Context\BlackfireContextTrait;

    class SomeContext extends RawMinkContext
    {
        use BlackfireContextTrait;

        /**
         * @Given I am on ":landingPage" landing page
         * @When I go to ":landingPage" landing page
         */
        public function iAmOnLandingPage($landingPage)
        {
            $this->disableProfiling();
            $this->visitPath("/$landingPage");

            // You may re-enable profiling and visit other pages
            $this->enableProfiling();
            $this->visitPath('/foo/bar');
        }
    }

.. note::

    If you use the Symfony driver, since no actual requests are made, Blackfire will interpret these profiles as coming
    from a command, not an HTTP request, so it will apply the assertions that you have defined for your commands,
    not your requests

Builds Comparison
-----------------

To :ref:`compare the current build to another one <assertions-comparisons>`,
you may set ``BLACKFIRE_EXTERNAL_ID`` and ``BLACKFIRE_EXTERNAL_PARENT_ID``
environment variables when launching your tests:

.. code-block:: bash

    BLACKFIRE_EXTERNAL_ID=current_build_reference \
    BLACKFIRE_EXTERNAL_PARENT_ID=parent_build_reference \
    vendor/bin/behat

.. note::

    You may use Git commit identifiers as references.

Disable the Blackfire Builds Globally
-------------------------------------

You may want to run Blackfire tests in a separate job in your pipeline, while
still running your functional tests.

In this case, it is possible to globally disable the Blackfire build by setting
the ``BLACKFIRE_BUILD_DISABLED`` environment variable to ``1``:

.. code-block:: bash

    BLACKFIRE_BUILD_DISABLED=1 vendor/bin/behat
