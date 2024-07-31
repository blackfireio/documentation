Triggering Profiles
===================

Profiles are the most extensive set of data that Blackfire can collect. They aim
to help you understand why a specific script behaves in a certain way and allow
you to identify the root cause of bottlenecks to the function or service call.

If you haven't done it yet, it's time to trigger your first profile and collect
that data. There are two ways to trigger a profile:

1. Using the browser extension:
    - Install the Blackfire browser extension for
      :doc:`Chrome</integrations/browsers/chrome>` or
      :doc:`Firefox </integrations/browsers/firefox>`.
    - Go to the website of your application.
    - Click on the Blackfire extension icon in your browser toolbar.
    - Click on the big red ``Profile!`` button.

2. Using the CLI:
    - The Blackfire CLI is bundled with :doc:`Blackfire agent</up-and-running/configuration/agent>`
      which means it is available on all devices that have Blackfire installed.
      To trigger a profile using the CLI, you should:

        - Profile a HTTP request:
            - ``blackfire curl <endpoint or curl command>``

        - Profile a command:
            - ``blackfire run php /foo/bar/baz --option=123``
            - ``blackfire run python foo_bar_baz.py``

.. note::

    :doc:`Know more about triggering profiles </profiling-cookbooks/index>`
