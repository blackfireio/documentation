Blackfire Player [level: Production]
====================================

:doc:`Blackfire Player </builds-cookbooks/player>` natively integrates
Blackfire profiler.

To use Blackfire Player with Blackfire profiler, add ``--blackfire-env`` option to
your ``blackfire-player`` command. You may use either the environment name or its UUID:

.. code-block:: bash

    blackfire-player run scenario.bkf --blackfire-env="Environment name or UUID"

.. note::

    To use Blackfire Player together with Blackfire Profiler,
    you need to correctly setup your client credentials, which are available
    at https://blackfire.io/my/settings/credentials

    The :doc:`Blackfire Player </builds-cookbooks/player>` documentation provides
    complete information on its configuration.

    .. include-twig:: `blackfire_player_with_env`

    Or, using a :ref:`fully configured alias <player-alias>`:

    .. include-twig:: `blackfire_player_with_env_alias`

Builds
------

The Blackfire Player creates a build to group all the scenarios.
Each scenario contains profiles and assertion reports for requests made in
each step of the executed scenario.

.. note::

    All requests are profiled by default. You can disable the profiler in a
    step or in a complete scenario by setting ``blackfire false``.

    .. code-block:: blackfire

        scenario
            name "Scenario with Blackfire"
            # Use the environment name (or UUID) you're targeting or false to disable
            blackfire true
            # ...

        scenario
            name "Scenario without Blackfire"
            # You can disable Blackfire support on the scenario, or only on some steps
            blackfire false
            # ...

.. _writing-blackfire-assertions:

Assertions
----------

All the assertions defined in ``.blackfire.yaml`` are automatically run
alongside :ref:`Blackfire Player expectations <writing-expectations>`.

You also may add assertions within a step with ``assert`` instruction:

.. code-block:: blackfire

    scenario
        visit url('/blog/')
            name "Blog homepage"
            assert main.peak_memory < 10M

:doc:`Any assertion supported in .blackfire.yaml
</testing-cookbooks/assertions>`, based on :doc:`built-in and/or custom metrics
</testing-cookbooks/metrics>`, can be added this way.

Using Blackfire Environment Variables
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can use assertions variables, defined in the Blackfire environment,
:ref:`like you would do within assertions defined in .blackfire.yaml file
<assertions-variables>`:

.. code-block:: blackfire

    scenario
        # no Twig template compilation in production
        # not enforced in other environments
        visit url('/blog/')
            name "Blog homepage"
            assert main.peak_memory < 10mb * var('memory_coeff')

.. _builds-comparison-player:

Builds Comparison
~~~~~~~~~~~~~~~~~

To :ref:`make some comparisons with a previous build
<assertions-comparisons>`, you can set the ``external_id`` and
``external_parent_id`` settings of the build by passing
``BLACKFIRE_EXTERNAL_ID`` and ``BLACKFIRE_EXTERNAL_PARENT_ID`` environment
variables:

.. code-block:: bash

    BLACKFIRE_EXTERNAL_ID=current_build_reference \
    BLACKFIRE_EXTERNAL_PARENT_ID=parent_build_reference \
    blackfire-player run scenario.bkf --blackfire-env=ENV_NAME_OR_UUID

Other Supported Instructions
----------------------------

Samples
~~~~~~~

The ``samples`` instruction tells Blackfire Profiler how many samples must be
aggregated for a single profile. The default value is ``1``.

Warmup
~~~~~~

The ``warmup`` instruction tells Blackfire Profiler whether to warmup the
requested URL first.

Its value can be:

* **true**: Warmups safe HTTP requests, or when the number of samples is
  more than one. Warmup will be executed 3 times. (default value)

* **A number**: Same behavior as **true**, but allows to change the number of
  warmup requests.

* **false**: Disables warmup

.. code-block:: blackfire

    scenario
        visit url('/blog/')
            name "Blog homepage"
            assert main.peak_memory < 10M
            samples 2
            warmup true
