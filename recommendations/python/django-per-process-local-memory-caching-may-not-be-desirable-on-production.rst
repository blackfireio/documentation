Django Per-Process Local-Memory Caching May Not Be Desirable On Production
==========================================================================

If you're using a cache, Django defaults to per-process local-memory caching
which may not be desirable on production. It would be a better practice to use 
a different cache backend on production.

See `local-memory caching`_ for more details.
See `Deployment Checklist for caches`_.

.. _`local-memory caching`: https://docs.djangoproject.com/en/3.1/topics/cache/#local-memory-caching
.. _`Deployment Checklist for caches`: https://docs.djangoproject.com/en/3.1/howto/deployment/checklist/#caches
