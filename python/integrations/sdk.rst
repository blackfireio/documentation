Python SDK [language: Python]
=============================

Installation
------------

The Blackfire Python SDK is available :doc:`with the Blackfire Python Package
</up-and-running/installation>`.

Blackfire Python SDK
--------------------

The **Blackfire Python SDK** allows you to generate profiles from your code and
eases the integration with third-party libraries.

The main entry point of the SDK is the ``blackfire`` module:

.. code-block:: python

    from blackfire import probe

The probe allows you to profile any parts of your code:

.. code-block:: python

    from blackfire import probe

    probe.initialize()
    probe.enable()

    # some Python code you want to profile

    probe.end()

.. _probe-configuration-python:

Configuring the Blackfire Probe Manually
----------------------------------------

The Blackfire Probe is :doc:`usually configured via environment variables
</python/configuration>`, but you can customize the configuration when calling
the ``initialize()`` method via optional parameters:

.. code-block:: python

   from blackfire import probe

   probe.initialize(
        # Client credentials. If None, they are read from environment variables, or config_file.
        client_id=None,
        client_token=None,
        # 1: error, 2: warning, 3: info, 4: debug
        log_level=None,
        # The destination of the log. i.e: /tmp/probe.log
        log_file=None,
        # Where to find the Blackfire CLI configuration file to retrieve the client_id and client_token values.
        config_file='~/.blackfire.ini',
        # The Blackfire Query, usually given by blackfire run or created on the fly by the SDK.
        query=None,
        # The network socket to use for contacting the agent
        agent_socket=None,
        # The connection timeout when connecting to the agent
        agent_timeout=None,
        # The Blackfire API endpoint
        endpoint=None,
    )

.. caution::

    Please note that ``log_file`` and ``log_level`` parameters are deprecated and
    removed in version ``1.10.0``. You can configure the log file and level
    via the ``BLACKFIRE_LOG_FILE`` and ``BLACKFIRE_LOG_LEVEL``
    :doc:`environment variables</python/configuration>`.


Instrumenting Code using a Context Manager
------------------------------------------

The SDK provides the ``run(call_end=True)`` method that simplifies the use of the
``enable()`` and ``disable()`` methods:

.. code-block:: python

    from blackfire import probe

    with probe.run():
        foo()
        bar()

is equivalent to:

.. code-block:: python

    from blackfire import probe

    probe.enable()
    try:
        foo()
        bar()
    finally:
        probe.disable()
        probe.end() # if call_end is True.

Instrumenting Code Using the Decorator
--------------------------------------

The SDK provides the ``@profile`` decorator, making it possible to profile
functions separately:

.. code-block:: python

    from blackfire import profile

    @profile
    def foo():
        import time
        time.sleep(1.0)

    foo()

In the snippet above, function ``foo()`` is using the ``@profile`` decorator.
A probe instance is created by the decorator, using the :doc:`configuration defined
by environment variables </python/configuration>`.

You may specify a pair of Client ID/Token in the decorator:

.. code-block:: python

    from blackfire import profile

    @profile(client_id = "my_client_id", client_token = "my_client_token")
    def foo()
        import time
        time.sleep(1.0)

    foo()

Controlling Automatic Instrumentation
-------------------------------------

.. code-block:: python

    from blackfire import probe

    probe.initialize()

Start profiling the code by calling ``enable()``:

.. code-block:: python

    # Start the profiling
    probe.enable()

Stop profiling the code by calling ``disable()``:

.. code-block:: python

    # Stop the profiling
    probe.disable()

You can call ``enable()`` and ``disable()`` as many times as needed in your
code. You can also discard any collected data by calling ``clear_traces()``.

Calling ``end()`` instead of ``disable()`` stops the profiling and forces the
collected data to be sent to Blackfire:

.. code-block:: python

    # Stop the profiling
    # Send the result to blackfire
    probe.end()

.. _sub-profiles-python:

Generating Sub-Profiles
-----------------------

Thanks to the :ref:`Distributed Profiling feature <distributed-profiling>`, you
can embed sub-profiles in the main profile.

For instance, when profiling command line programs that call sub-processes, you
might want to trigger profiles for them as well. You can do so by generating a
sub-profile request:

.. code-block:: python

    import subprocess
    import sys
    import os
    from blackfire import probe

    probe.initialize(
        client_id='xxxx',
        client_token='xxxx'
    )

    with probe.run():
        env = os.environ.copy()
        env['BLACKFIRE_QUERY'] = probe.generate_subprofile_query()
        _ = subprocess.run([sys.executable, "my_subprocess.py"], env=env)

Sub-profiles also work for HTTP requests by adding a ``X-Blackfire-Query`` HTTP
header.

.. code-block:: python

    import requests
    from blackfire import probe

    with probe.run():
        url = 'https://mycustomapi.com'
        headers = {'X-Blackfire-Query:': probe.generate_subprofile_query()}
        r = requests.get(url, headers=headers)


.. note::

    The target process or HTTP server being sub-profiled may be written in any
    language supported by Blackfire.

Adding a Marker to the Timeline View
------------------------------------

With Markers, you can :ref:`add cue-points to the Timeline
View <timeline-markers>`. This can be done by adding the following instruction
in your code, where you want to add such a cue-point:

.. code-block:: python

    from blackfire import probe
    probe.add_marker('My Marker Label')

Profiling multiple threads simultaneously
-----------------------------------------

Every SDK API call works under thread boundaries: enabling a profiler via
`probe.enable()` enables it only for the current thread executing the API call.
Same is true for other API calls as well: e.g., `probe.initialize()`,
`probe.end()`...etc.

One  interesting use case example of this feature might be to profile each worker
thread individually in your favorite task queue, such as Celery.

As of version `1.14.0+`, multiple threads can be profiled simultaneously.

For example, you can call `probe.enable()` or `probe.end()` in different threads at
the same time and in the same process. The profiler will handle the underlying
segregation and aggregation of the profiling results.

This example profiles multiple threads simultaneously using the Sub-Profiles API:

.. code-block:: python

    from blackfire import probe

    THREAD_COUNT = 5

    def _thread_worker(i, query):
        probe.initialize(query=query, title="thread-%d" % (i))
        probe.enable()
        # do stuff in worker thread
        probe.end()


    probe.initialize(title="main-thread")
    probe.enable()
    # do stuff in main thread
    probe.end()
    ts = []
    for i in range(THREAD_COUNT):
        query = probe.generate_subprofile_query()
        t = threading.Thread(target=_thread_worker, args=(
            i + 1,
            query,
        ))
        t.start()
        ts.append(t)
    for t in ts:
        t.join()


This example generates a single profile, belonging to ``main-thread``, and
multiple linked :ref:`Sub-Profiles <distributed-profiling>`.

