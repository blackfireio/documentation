Configuring Blackfire Continuous Profiler for Python [level: Production]
=========================================================================

The Python continuous profiling is currently made accross 5 dimensions:

- **CPU Time**: time spent running on the CPU

- **Wall-time**: elapsed time per function call

- **Heap Live Size**: number of bytes allocated that are not yet garbage collected

- **Allocated memory**: number of bytes allocated in memory

- **Allocations**: time spent running on the CPU

Requirements
------------

- Python >= 3.7.O

- Blackfire Agent >= 2.13.0

Installation
------------

Get the `Blackfire Continuous Profiler Python library <https://github.com/blackfireio/python-continuous-profiling>`_:

.. code-block:: bash

    pip install blackfire_conprof

Python continuous profiler API
________________________________

The Python profiler API ``Profiler`` can be initiated with following options:

- ``application_name``: the application name.

- ``period``: specifies the length at which to collect CPU profiles.
  The default is 45 seconds.

- ``upload_timeout``: observability data upload timeout. The default is 10 seconds.

- ``labels``: a dict containing the custom labels specific to the profile payload that is sent.


The Python continuous profiler API has two functions:

.. code-block:: python

    def start():
    def stop():


``def start():``
~~~~~~~~~~~~~~~~~

The ``start`` function starts the continuous profiler probe.
It collects profiling information in the background and periodically uploads it
to the Blackfire Agent until the ``stop`` function is called.


``def stop():``
~~~~~~~~~~~~~~~~

Stops the continuous profiling probe.


A simple example application
_____________________________

1/ Get the Blackfire Continuous Profiler Python library:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

    pip install blackfire_conprof

2/ Create `example.py` with the following code:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: python

    from blackfire_conprof.profiler import Profiler

    def foo():
        import time
        time.sleep(1.0)

    profiler = Profiler(application_name="my-python-app", labels={'my-extra-label': 'data'})
    profiler.start()
    foo()
    profiler.stop()

3/ Run the example application:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

    python example.py

