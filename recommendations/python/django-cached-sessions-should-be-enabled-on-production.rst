Django Cached Sessions Should Be Enabled On Production
======================================================

Using a cache-based session backend improves performance so it is advised to use
cached sessions on production.

A local-memory cache backend doesn't retain data long enough to be a good choice 
for caching session. More details on selecting appropiate cache backend for 
sessions can be found in `Using cached sessions`_ documentation.

See `Deployment Checklist for sessions`_ for more details.

.. _`Using cached sessions`: https://docs.djangoproject.com/en/3.1/topics/http/sessions/#cached-sessions-backend
.. _`Deployment Checklist for sessions`: https://docs.djangoproject.com/en/3.1/howto/deployment/checklist/#sessions
