Nginx
=====

If you are using Nginx as a reverse-proxy cache, and as described in the
:doc:`reverse proxies documentation section </up-and-running/reverse-proxies>`,
you must bypass Nginx cache rules when profiling.

The instruction you must add to your Nginx configuration file depends on the
Nginx module you are using.

**Using http_fastcgi module**

.. code-block:: nginx

    fastcgi_cache_bypass $http_x_blackfire_query;
    fastcgi_pass_request_headers on;

.. note::

    You may `refer to the http_fastcgi module documentation
    <https://nginx.org/en/docs/http/ngx_http_fastcgi_module.html#fastcgi_cache_bypass>`_.

**Using http_proxy module**

.. code-block:: nginx

    proxy_cache_bypass $http_x_blackfire_query;
    proxy_pass_request_headers on;

.. note::

    You may `refer to the http_proxy module documentation
    <https://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_cache_bypass>`_.
