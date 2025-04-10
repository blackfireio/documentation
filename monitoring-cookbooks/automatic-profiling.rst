Automatic Profiling
===================

.. include-twig:: `youtube-iframe`
    :title: introduction-to-blackfire
    :src: https://www.youtube-nocookie.com/embed/-1aG-d7O8Vs?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Blackfire offers three levels of insights into your application performance:

* **Simple traces**: those collect high-level metrics, including overall response
  time and peak memory usage of a request (close to no overhead);

* **Extended traces**: those collect key metrics on your code, including
  the most significant calls, SQL queries, etc (low overhead); they result in
  "Spans" in a mini-timeline within a transaction view;

* **Profiles**: do collect the finest details on your application behavior, including
  Wall-time, I/O, CPU, Memory, Network, HTTP, SQL, at the function call level
  (highest overhead).

It is recommended to avoid practices that would involve profiling actual end-user
requests to avoid adding the profiling overhead on those (:ref:`read more
about the profiling overhead <understanding-blackfire-overhead>`).
We do recommend that you :doc:`profile regularly your application manually
</profiling-cookbooks/index>`, as well as :doc:`automatically through Builds
</builds-cookbooks/index>`

However, profiling actual end-user requests also offers additional "real-life"
context which may show valuable information to spot and debug a particular
issue.

While monitoring performance on a production server, profiles can be triggered
with two methods:

* The "Profile Next Request" feature;

* Blackfire's profiling automation of the most impactful requests.

.. _monitoring_profile_next_request:

Profile Next Request
--------------------

This feature is activated at the transaction level. Browse to a transaction
view and find the "Profile Next Request" button.

Once configured the next matching request on your production server will be
profiled.

.. caution::

    Profile Next Request won't work for :ref:`unnamed transactions
    <monitoring_unnamed_transactions>` or :ref:`transactions named from the UI
    <monitoring_naming_transactions_from_ui>`.

    You may ensure that transactions are :ref:`properly programmatically identified
    <monitoring_naming_transactions_programmatically>`.

.. _monitoring_automatic_profiling:

Automatic Profiling
-------------------

Blackfire **automatically triggers profiles on the ten most impactful transactions,
once per day**.

Note that such profiles are triggered on end-user requests. It may generate some
overhead, though only for those 10 requests per day.

Doing so enables Blackfire to collect :doc:`recommendations
</testing-cookbooks/recommendations>` for the top ten most impactful transactions,
and offers actionable insights to help you optimize your code.

.. caution::

    Automatic profiling is not triggered on :ref:`unnamed transactions
    <monitoring_unnamed_transactions>` and :ref:`transactions named from the UI
    <monitoring_naming_transactions_from_ui>`.

    You may ensure that transactions are :ref:`properly programmatically identified
    <monitoring_naming_transactions_programmatically>`.

Pre transaction detection
-------------------------

When profiles are generated using automatic profiling based on a transaction
name, the callgraph shows a ``Pre-transaction detection`` node, and the timeline
a ``Pre-transaction detection`` span.

Blackfire verifies upon reception of each request if it should be automatically
profiled. The detection of the transaction from the request
may require that some of the code is being executed. All of that code is
therefore not profiled and is represented at ``Pre-transaction detection``.
