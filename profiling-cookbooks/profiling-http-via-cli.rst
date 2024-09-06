Profiling HTTP Requests with the CLI
====================================

Blackfire lets you profile HTTP requests like web pages, web service calls, or
API calls.

To get started, check that you have Blackfire :doc:`installed
</up-and-running/installation>` correctly on the server hosting the website you
want to profile.

Profiling an HTTP request means instrumenting the project's code. Blackfire is
apart from many other profilers because of two main differences:

* Blackfire **automatically** instruments your code when needed, so you don't
  need to change your code;

* Blackfire does nothing when you are not profiling a request (the overhead is
  then almost zero), so it is safe to deploy Blackfire on production servers,
  even for heavy-traffic projects.

This cookbook describes how to profile from the command line interface. You can
also profile web applications from a :doc:`browser
</profiling-cookbooks/profiling-http-via-browser>`.

Profiling Simple HTTP Requests
------------------------------

Profiling an HTTP request can be done on the command line thanks to the
``blackfire`` utility.

The easiest way to profile an HTTP request is to use the ``curl`` sub-command
of the ``blackfire`` utility. It accepts the `same arguments and options
<https://curl.haxx.se/docs/manpage.html>`_ as the regular ``curl`` utility:

.. code-block:: bash

    blackfire curl http://example.com/

.. include:: _cli-profiling-warning.rst

You can get a list of options available for the ``curl`` sub-command:

.. code-block:: bash

    blackfire help curl

At the end of the request, ``blackfire`` outputs the URL where the profile can
be found (hide it by passing the ``-q`` option.)

.. sidebar:: Profiling without cURL

    Note that you need ``curl`` to be installed on your system for ``blackfire curl``
    to work. If ``curl`` is not available or if you prefer to use
    another tool to make your HTTP requests, use the ``run`` sub-command
    instead:

    .. code-block:: bash

        blackfire run sh -c 'curl -H "X-Blackfire-Query: $BLACKFIRE_QUERY" http://example.com/ > /dev/null'

        blackfire run sh -c 'wget --header="X-Blackfire-Query: $BLACKFIRE_QUERY" http://example.com/ > /dev/null'

    As you can see, you need to add a custom ``X-Blackfire-Query`` HTTP header
    to trigger the profiling; the value is the content of the
    ``$BLACKFIRE_QUERY`` environment variable, which is automatically set by
    the ``blackfire`` utility. It means that this method works for any tools
    that accept custom HTTP headers.

JSON Output
~~~~~~~~~~~

You can integrate Blackfire results into your tools by using the ``--json``
option to get a JSON representation of a profile:

.. code-block:: bash

    blackfire --json curl http://example.com/

.. note::

    The JSON output is displayed on ``STDOUT``, while the regular output (e.g.
    progress, profile summary...) is displayed on ``STDERR``.

The resources consumed are available under the ``envelope`` entry;
keys are the cost dimensions:

* **pmu**: Peak Memory Usage (in bytes);
* **nw**: Network (in bytes);
* **wt**: Wall Clock Time (in microseconds);
* **cpu**: CPU time (in microseconds);
* **io**: I/O time (in microseconds).

.. _profile_post_ajax_more:

Profiling non-GET Requests, Ajax, and More
------------------------------------------

Profiling non-GET requests or requests which need some specific HTTP headers is
no different as ``blackfire curl`` supports all cURL options:

.. code-block:: bash

    blackfire curl -XPOST http://example.com/

Profiling Part of an HTTP Call
------------------------------

Blackfire automatically instruments your code, but sometimes, you might want to
focus the profiling on only part of the code. That's possible when opting for
:ref:`manual instrumentation via the PHP SDK <php-sdk-manual-instrumentation>`.

After instrumenting your code, use the ``blackfire`` utility as above to
profile your application. When not using Blackfire, all calls are converted to
*no-ops*.

Profiling all Requests While you Browse
---------------------------------------

Profiling POST requests, Ajax requests, and API calls can be done
via the ":ref:`Profile all requests <profiling-all-requests>`" link in the
browser extension.

When profiling from a browser, select "Profile all requests", then "Record!".
Blackfire will instrument all requests until you click on the "Stop"
button in the pop-over.

A pop-over window will open at the bottom right of your screen,
where all profiled requests will be listed.

All PHP requests which have been profiled will be shown on your
:route:`dashboard <dashboard>`.

.. include:: _profiling-all-request-chrome-warning.rst
