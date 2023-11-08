Symfony sub-requests should be replaced by ESI in production
============================================================

In Symfony applications, sub-requests are simulated requests performed internally
by Symfony to call one or more controllers in the same request. Sub-requests are
a very convenient way to `embed controllers in a template`_.

However, performing sub-requests can increase the response time of the
application significantly. Therefore, the application should not make any sub-
request in the production server. Instead, sub-requests should be served by a
reverse proxy such as `Varnish`_ using `ESI`_ (Edge Side Includes), which allows
to define a separate caching strategy for each sub-request.

.. _`embed controllers in a template`: https://symfony.com/doc/current/templating/embedding_controllers.html
.. _`Varnish`: https://varnish-cache.org
.. _`ESI`: https://symfony.com/doc/current/http_cache/esi.html
