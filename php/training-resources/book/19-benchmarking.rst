Chapter 19 - Benchmarking
=========================

Web applications are not just about generating web pages or API payloads. The
heart of an application is its custom business logic. The business logic is the
code that is reused in all parts of a project: from generating data for mobile
apps to fueling web frontends. This is also the code that should be decoupled
from your framework of choice as it should survive refactoring and technology
changes. Making this code fast will pay off in the long run.

An application's business logic often relies on non-trivial algorithms that can
significantly affect the entire application's performance. The best way to
determine which implementation of a given algorithm is faster is to use a
benchmarking tool to complement Blackfire.

Blackfire can be used to understand the reasons why an algorithm is faster or
slower than another one by using manual instrumentation. A benchmarking tool
provides the infrastructure to run different algorithms in isolation and answer
questions like which algorithm is better? Better is not always faster as using
the ideal algorithm is usually a trade-off between CPU cycles and memory usage.
A good benchmarking tool also provides tools for analyzing the generated
statistics and guides you in analyzing the results.

In the PHP world, `PHPBench <https://phpbench.readthedocs.io/>`_ is such a
tool. PHPBench goes beyond simple benchmarks as it promotes writing
long-lasting benchmarks that you can keep alongside your code and your tests.

Similar to how you create a test class for your testing framework, create a
bench class for your benchmarking framework:

.. code-block:: php

    class SomeBench
    {
        public function benchAlgorithm()
        {
            // call the code you want to benchmark
        }
    }

Running the bench is then a matter of using the ``phpbench`` utility:

.. code-block:: bash

    phpbench run benchmarks/SomeBench.php --report=default

PHPBench supports many options to configure the number of iterations, data
providers, before/after tasks to setup and tear down benchmarks, and more.
