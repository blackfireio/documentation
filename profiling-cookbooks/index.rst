Profiling Cookbooks
===================

.. include-twig:: `youtube-iframe`
    :title: introduction-to-blackfire
    :src: https://www.youtube-nocookie.com/embed/iCyqQ4spubE?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Blackfire's deterministic profiler precisely measures how your :doc:`PHP </php/index>`
and :doc:`Python </python/index>` applications consume resources during execution,
capturing an extensive set of multidimensional observability data.

This enables you to thoroughly discover performance bottlenecks and gain deep
insights into your code's runtime behavior.

The Blackfire profiler can be seamlessly deployed across all your
:doc:`environments </reference-guide/environments>` without any changes required
in your application code or additional steps to remove instrumentation before
releasing.

Moreover, Blackfire ensures there is no performance impact on production end-users,
as profiling overhead only applies to the specific requests initiated by developers.

.. toctree::
    :maxdepth: 2
    :titlesonly:

    profiling-http-via-browser
    profiling-http-via-cli
    profiling-cli
    profiling-microservices
    distributed-profiling
    debugging
    sharing-profiles
    understanding-call-graphs
    understanding-comparisons
    understanding-timelines
    understanding-http-requests
    profiling-usage
    tips
