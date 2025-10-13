Browsing Browser Traces
=======================

Browser Monitoring now lets you **explore individual traces** to investigate
specific user sessions.

Accessing Trace Details
-----------------------

Click **Browse Trace** in the **Browser Overview** section to open a detailed
trace view.

Each trace represents a user visit, including page loads, navigation events, and
fetched resources.

.. image:: ../images/front-end/browse-traces-1.png
    :align: center
    :alt: Accessing a single browser monitoring trace


You can:

- Move between traces using the Previous/Next buttons.
- View session details such as platform, browser version, country, screen size, and timestamp.
- Inspect each fetched resource (span) to understand how it was loaded.

.. image:: ../images/front-end/browse-traces-2.png
    :align: center
    :alt: Accessing a single browser monitoring trace

.. image:: ../images/front-end/browse-traces-3.png
    :align: center
    :alt: Displaying the different spans of a single browser monitoring trace

- Hover over a span to see technical details such as:
    - Resource type and URL
    - Transfer size and compression rate
    - DNS lookup, TCP handshake, and wait times
    - Download duration

.. image:: ../images/front-end/browse-traces-5.png
    :align: center
    :alt: Hovering a span

Depending on the trace, some or all of these breakdowns may be available.

Visitor Journey
---------------

For Single-Page Applications (SPA) or multi-page flows, the trace view also
provides a Visitor Journey timeline.

.. image:: ../images/front-end/browse-traces-4.png
    :align: center
    :alt: Displaying the visitor journey

This shows the sequence of user interactions and navigation events during the
session, allowing you to correlate specific performance behaviors with the exact
user journey.
