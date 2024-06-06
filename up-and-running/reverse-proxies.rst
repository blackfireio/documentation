Bypassing Reverse Proxy, Cache, and Content Delivery Networks (CDN)
===================================================================

When using a reverse proxy (Varnish, Fastly, HA Proxy, Nginx...), a load
balancer or a content delivery network (CDN) sitting in front of your
application, you need to bypass them when profiling with Blackfire.

In such context, your infrastructure **must**:

* Serve a **non-cached** response;
* **Not remove the specific HTTP headers** injected by the Blackfire browser
  extension, the Blackfire CLI client, or the Blackfire Player (read further
  below);
* **Target a specific server** running your application, behind the proxy.

.. _reverse-proxies-headers:

HTTP Headers
------------

In order to successfully profile your application, several HTTP headers are
processed by the client. These headers are required to pass through to and
from your application (and the Blackfire probe).

Request Headers
~~~~~~~~~~~~~~~

Any Blackfire client, whether it is the Blackfire browser extension, the
Blackfire CLI client, or the Blackfire Player, injects a specific HTTP header
into each Request to profile a resource: ``X-Blackfire-Query``. This header
contains mandatory information for the probe, including the signature (read
:ref:`How does Blackfire work for further details <how-does-blackfire-work>`).

Response Headers
~~~~~~~~~~~~~~~~

The following HTTP response headers need to be preserved:

* ``X-Blackfire-Response``
* ``X-Blackfire-Error``

Those headers are needed by the Blackfire clients.

.. _configuration-load-balancer:

Load Balancer
-------------

If you are using multiple application servers behind a load-balancer:

 - Install the **Blackfire Probe** and the **Blackfire Agent** on every server;

Reverse Proxies and CDNs
------------------------

We provide various integration examples with different reverse proxies and CDNs:

* :doc:`Varnish </integrations/proxies/varnish>`
* :doc:`Fastly </integrations/proxies/fastly>`
* :doc:`Cloudflare </integrations/proxies/cloudflare>`
* :doc:`Nginx </integrations/proxies/nginx>`
