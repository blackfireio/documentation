PHPUnit [language: PHP]
=======================

The :doc:`Blackfire PHP SDK </php/integrations/sdk>` provides a simple and
powerful integration with PHPUnit.

Any regular PHPUnit test class (extending ``PHPUnit\Framework\TestCase``) can
use Blackfire to execute assertions on a snippet of code:

.. code-block:: php

    use Blackfire\Bridge\PhpUnit\TestCaseTrait;
    use Blackfire\Profile;
    use PHPUnit\Framework\TestCase;

    class IntegrationTest extends TestCase
    {
        use TestCaseTrait;

        /**
         * @group blackfire
         * @requires extension blackfire
         */
        public function testSomething()
        {
            $config = new Profile\Configuration();

            // define some assertions
            $config
                ->assert('metrics.sql.queries.count < 5', 'SQL queries')
                ->assert('metrics.twig.render.count < 3', 'Rendered Twig templates')
                ->assert('metrics.twig.compile.count == 0', 'Twig compilation')
                // ...
            ;

            $profile = $this->assertBlackfire($config, function () {
                // do something that you want to profile
                // and assertions are going to be executed against it
            });
        }
    }

When running the above test, Blackfire will automatically instrument the
wrapped code and execute the assertions defined by the ``Configuration``
instance. If the assertions fail, a regular PHPunit error is generated and the
output gives all the details you need:

.. code-block:: text

    There was 1 failure:

    1) IntegrationTest::testSomething
    Failed asserting that Blackfire tests pass.
    1 tests failures out of 2.

        failed: 1 write calls
          - metrics.twig.compile 2 == 0

    More information at https://blackfire.io/profiles/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/graph.

    /.../vendor/blackfire/php-sdk/src/Blackfire/Bridge/PhpUnit/TestConstraint.php:60
    /.../vendor/blackfire/php-sdk/src/Blackfire/Client.php:90
    /.../Tests/IntegrationTest.php:56

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

.. note::

    The PHP SDK being used under the hood, profiles triggered from a unit test
    won't be listed in your dashboard. :ref:`You can force them to be listed by
    disabling *skip_timeline* metadata <php-sdk-profile-configuration>`.

.. note::

    For PHP 5.3, where traits are not supported, you can use the now deprecated
    ``assertPhpUnit()`` method:

    .. code-block:: php

        use Blackfire\Client;
        use Blackfire\Profile;
        use PHPUnit\Framework\TestCase;

        class IntegrationTest extends TestCase
        {
            private $blackfire;

            /**
             * @group blackfire
             * @requires extension blackfire
             */
            public function testSomething()
            {
                $config = new Profile\Configuration();

                // define some assertions
                $config
                    ->assert('metrics.sql.queries.count < 5', 'SQL queries')
                    ->assert('metrics.twig.render < 3', 'Rendered Twig templates')
                    ->assert('metrics.twig.compile == 0', 'Twig compilation')
                    // ...
                ;

                $profile = $this->getBlackfireClient()->assertPhpUnit($this, $config, function () {
                    // do something that you want to profile
                    // and assertions are going to be executed against
                });
            }

            private function getBlackfireClient()
            {
                if (null === $this->blackfire) {
                    $this->blackfire = new Client();
                }

                return $this->blackfire;
            }
        }

To avoid making your tests fail in case Blackfire is not available, add the
``@requires extension blackfire`` annotation on tests using Blackfire (tests
will then be automatically skipped when the Blackfire PHP extension is not
installed or enabled).

It's also a good practice to make all Blackfire tests parts of a specific
PHPUnit group like ``@group blackfire`` as they are probably slower than
regular tests.

Last, but not least, try to **avoid writing assertions relying on time**
(wall clock time, CPU time, or I/O time). Assertions on time are volatile and
can make your tests fail randomly. Instead, try to define :ref:`custom metrics
<metrics-custom-metrics>` and :doc:`write assertions
</testing-cookbooks/assertions>` on them to test the behavior of the code that
might slow things down (like in the above example where we check that no Twig
template is compiled or that the number of SQL statements executed is limited).

.. _testing-legacy-code:

Testing Legacy Code
-------------------

Using Blackfire in a PHPUnit test is also a great way to test some legacy
code that is difficult to test otherwise. As Blackfire is aware of all the
function calls made by your code, you can define metrics on some key ones
and assert that they are called or not depending on your expectations.

As a simple example, imagine a code where there is a cache layer managed by
a ``Cache`` class. You might want to test that after the cache is primed,
the cache is used:

.. code-block:: php

    $config
        ->defineMetric(new Profile\Metric('cache.write_calls', '=Cache::write'))
        ->defineMetric(new Profile\Metric('cache.read_calls', '=Cache::read'))
        ->assert('cache.write_calls.count == 0')
        ->assert('cache.read_calls.count > 0')
    ;

Learn more about :ref:`defining your metrics <metrics-custom-metrics>`.

.. tip::

    If you run your PHPUnit tests with `Travis CI <https://travis-ci.com/>`_,
    read :doc:`how to configure it </integrations/ci/travis>`.
