Chapter 12 - Forget about Time in your Tests
============================================

Writing good assertions is a difficult task. The easiest test you can think of
probably involves the wall time or the memory, but assertions on these
dimensions are actually very weak. **Time is not a stable metric**. External
factors such as machine load can have significant impacts on wall time between
two profiles of identical code. Volatile tests must be avoided at all costs as
they make your test suite less reliable and degrade the trust your team has in
any failures.

.. _forget-about-time:

Forget about Time
-----------------

**Avoid writing assertions that depend on time**. When running a piece of code,
**time is just a consequence** of what happened in the code. Look deeper.
Understanding which functions were called at runtime is exactly what a profiler
is good at.

**Use time to identify the slow parts in your code and then write assertions on
the root cause.**

A typical example is a micro-service architecture where the number of HTTP
requests on external web services is likely to be the main performance issue.
The more HTTP requests you have in the code, the slower the code is going to
be. The number of external requests is a stable value and it should not change
between two profiles generated from the same codebase. Thus, limiting the
number of HTTP requests allowed for a project is a great way to ensure good
code performance:

.. code-block:: yaml

    # fragile, might break from time to time
    - main.wall_time < 50ms

    # robust, the real root cause for slowness
    - metrics.http.requests.count < 5

Tests Best Practices
--------------------

We already used such an approach when we wrote assertions for Finding Bigfoot
and phpmd:

.. code-block:: yaml

    # limit the number of sub-processes (using the built-in metric)
    - metrics.symfony.processes.count < 10

    # be sure we don't hit the cache more than needed
    - metrics.parses.count == metrics.cache_driver.count

You can also limit the number of SQL queries:

.. code-block:: yaml

    - metrics.sql.queries.count < 10

What is the ideal number? 5? 10? It really depends on your project. As you
know, the fastest code is the code that is never called. Checking that a
function is never called is also a very good practice.

Websites with a lot of traffic might want no SQL queries on their homepage:

.. code-block:: yaml

    - metrics.sql.queries.count == 0

Another best practice for any website is to never send emails synchronously:

.. code-block:: yaml

    - metrics.emails.sent.count == 0

Some more examples on popular PHP libraries:

.. code-block:: yaml

    # check that the Twig C extension is installed
    - metrics.twig.attributes.php.get.count == 0

    # limit the number of DB connections
    # can be 2 if you have a specific connection for the session
    - metrics.sql.connections.count <= 1

    # same for Redis and AMQP
    - metrics.redis.connections.count <= 1
    - metrics.amqp.connections.count <= 1

Another good practice for production servers is to generate all cached files
before a deployment goes live. The following assertions check this assumption:

.. code-block:: yaml

    # no Twig/Smarty compilation
    - is_dev() or metrics.twig.compile.count == 0
    - is_dev() or metrics.smarty.compile.count == 0

    # no Symfony metadata checks
    - is_dev() or metrics.symfony.config_check.count == 0

    # no Doctrine parsing
    - is_dev() or (metrics.doctrine.annotations.parsed.count + metrics.doctrine.annotations.read.count + metrics.doctrine.dql.parsed.count + metrics.doctrine.entities.metadata.count + metrics.doctrine.proxies.generated.count) == 0

    # no YAML loaded
    - is_dev() or metrics.symfony.yaml.reads.count == 0

    # Assetic controller must not be called (assets should be dumped)
    - is_dev() or metrics.assetic.controller.calls.count == 0

The ``is_dev()`` function returns ``false`` when the assertion is run in an
environment configured for production usage.

.. sidebar:: Are you sure that your last Code Change works?

    Back in 2016, I decided to install the Twig C extension on `symfony.com
    <https://symfony.com/>`_ servers. It took me less than 5 minutes. For good
    measure, I added the ``twig.attributes.count == 0`` assertion in my
    Blackfire tests and run a profile... it failed. I double-checked, and I
    forgot to symlink the new ``twig.ini`` configuration I created to the
    PHP-FPM directory. Easy enough to fix.

    But the assertion kept failing. I forgot that at the same time, I also
    changed the cache directory for Twig templates and PHP was still using the
    old directory. Again, easy enough to fix.

    It took me two or three attempts before I got a green tick from Blackfire.
    Without Blackfire, I would never have noticed that the C extension was
    installed but not enabled properly.

**Blackfire promotes a metrics-first approach to performance**. Write good
assertions and they will catch problems before you ever need to analyze a call
graph.

Don't be afraid to create custom metrics. This is where Blackfire shines. The
ability to create custom assertions based on your team's code patterns is a
powerful tool. Reusing a custom metric on an Open-Source library often?
:route:`Contact us <contact-us>` and we will consider adding it to our built-in
repository of metrics.

Performance Recommendations
---------------------------

Writing tests is hard as it requires you to find the relevant and actionable
metric and to know what is an acceptable value for that metric. But for common
frameworks and PHP itself, Blackfire gives you a head start via recommendations!

Performance recommendations are "default" tests that are always run. These tests
were written by PHP experts. Anytime you profile your application, if one of
those tests fails, you will be warned directly on the profile view. Besides
recommendations on PHP itself, Blackfire has solid recommendations for major
projects like Symfony, Magento, Drupal, Ibexa and TYPO3.

Each recommendation comes with a documentation page that explains why it was
written, and how you can fix the issue. If you believe that some recommendations
are false positives or not applicable, you can always discard them.

Blackfire goes one step further as recommendations are not just for performance.
We worked on a set of quality and security best practices, which we implemented
as default tests as well.

Quality recommendations aim specifically at making sure that your are pushing
the right configuration in production, for instance that your ``php.ini`` file
and the cache settings are optimized.

Security recommendations help you make sure that you don't push un-secure code
or configuration to production. For instance, Blackfire checks if your
dependencies have known security vulnerabilities. Most tools that check security
issues require you to push some code, but what about that live website which has
been running for months with no changes? Check chapter 16 to see how to let
Blackfire run automatically and let you know!

.. note::

    We are very open to improving recommendations, or adding more of them. If
    you have an expertise that you would like to share, don't hesitate to
    :route:`reach out to us <contact-us>`!

Conclusion
----------

Time makes it easier to find the root cause of a performance issue, but it is a
poor metric when it comes to performance assertions.

Having the appropriate metrics makes it possible to capture a lot of information
about your code, PHP, or any framework you might rely on. And the possibilities
are then huge.

Have you realized that most of the assertion examples are related to code
behavior rather than performance? Blackfire is not just about performance.
Blackfire can be used in an unexpected way: understanding how code works at
runtime. This is a fascinating usage, which we will study in the next chapter.
