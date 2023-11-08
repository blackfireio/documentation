Chapter 20 - Load-Testing
=========================

Code behavior depends on many factors, including server load. Understanding the
impact of server load will prove useful when trying to optimize the performance
of a codebase. Simulating load can be done via specialized Open-Source tools
like `JMeter <https://jmeter.apache.org/>`_ or `Gatling <https://gatling.io>`_
and by online services that can provision huge numbers of virtual machines that
simulate a high number of users.

Load-testing tools work by simulating user sessions browsing your application
for a period of time. These statistics can provide some insight, but they
cannot explain why your code becomes slower when it is under stress. One way to
get more information is to run some Blackfire scenarios (via `Blackfire player
<https://blackfire.io/docs/builds-cookbooks/player>`_) while the load is high
and compare these profiles with ones generated under negligible load. The
comparison graph should highlight which parts of the code degrade under stress.

.. tip::

    Instead of using the JMeter GUI to create scenarios, use a recorder like
    the one provided by `Blazemeter
    <https://guide.blazemeter.com/hc/en-us/articles/206732579-Chrome-Extension>`_.
