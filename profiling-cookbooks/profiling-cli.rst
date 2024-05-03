Profiling CLI Commands
======================

Blackfire can profile any code that you need to run on the command line thanks
to the ``blackfire`` utility that is bundled with the :ref:`Blackfire Agent
<installation-instructions>`.

Profiling Simple CLI Scripts
----------------------------

Profiling a PHP script is a matter of prefixing your command with ``blackfire
run``:

.. code-block:: bash

    $ blackfire run php my-script.php
    $ blackfire run php my-script.php --your-script-options and arguments

At the end of the execution, ``blackfire`` outputs the URL where the profile
can be found (this can be hidden by passing the ``-q`` option.)

.. include:: _cli-profiling-warning.rst

JSON Output
~~~~~~~~~~~

You can integrate Blackfire results into your tools by using the ``--json``
option to get a JSON representation of a profile:

.. code-block:: bash

    $ blackfire --json run php my-script.php

.. note::

    The JSON output is displayed on ``STDOUT``, while the regular output (e.g.
    progress, profile summary...) is displayed on ``STDERR``.

The resources consumed are available under the ``envelope`` entry; keys are the
dimensions:

* **pmu**: Peak Memory Usage (in bytes);
* **nw**: Network (in bytes);
* **wt**: Wall Clock Time (in microseconds);
* **cpu**: CPU time (in microseconds);
* **io**: I/O time (in microseconds).


.. _profiling-cli-specifying-target-environment:

Specifying the Target Environment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When using ``blackfire run`` within a Development or Production subscription, you
can share the profiling result with your team. To do so, you will need
to specify the targeted :doc:`environment </reference-guide/environments>` with
the ``--env`` option:

.. code-block:: bash

    $ blackfire --env <env-uuid> run php my-script.php

Profiling Part of a CLI Script
------------------------------

Blackfire automatically instruments your code, but sometimes, you might want to
focus the profiling on only part of the code. That's possible when opting for
:ref:`manual instrumentation via the PHP SDK <php-sdk-manual-instrumentation>`.

After instrumenting your code, use the ``blackfire`` utility as above to
profile your application. When not using Blackfire, all calls are converted to
*no-ops*.

Profiling Consumers and Daemons
-------------------------------

Consumers and Daemons are special as they run for a very long time (or
indefinitely for daemons). In that case, using automatic instrumentation and
the ``blackfire`` utility cannot work. Fortunately, the :doc:`PHP SDK
</php/integrations/sdk>` provides an abstraction that lets you :ref:`profile
consumers and daemons <php-sdk-profiling-consumers-daemons>`.
