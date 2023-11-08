Profiling Micro-services [level: Production]
============================================

Blackfire supports profiling micro-service architectures out of the box,
thanks to a feature called :ref:`Distributed Profiling
<distributed-profiling>`.

When profiling a service, all HTTP and/or CLI services interacting with it are
also profiled (*sub-profiles* in Blackfire).

The main requirement is to have :doc:`Blackfire enabled
</up-and-running/installation>` on all machines which serve the profiled
requests.

Read more about :ref:`Distributed profiling <distributed-profiling>`.
