Django Cached Template Loader Should Be Enabled On Production
=============================================================

Enabling the cached template loader often improves performance drastically, as
it avoids compiling each template every time it needs to be rendered. The cached
loader stores the compiled templates in memory. It should be enabled on production.

See `Cached Template Loader`_ for more details on how to enable and use it.
See `Deployment Checklist for cached template loaders`_ for more details.

.. _`Cached Template Loader`: https://docs.djangoproject.com/en/3.1/ref/templates/api/#django.template.loaders.cached.Loader
.. _`Deployment Checklist for cached template loaders`: https://docs.djangoproject.com/en/3.1/howto/deployment/checklist/#templates
