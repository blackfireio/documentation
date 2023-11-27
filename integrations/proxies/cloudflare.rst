Cloudflare
==========

`Cloudflare <https://www.cloudflare.com>`_ is a content delivery network (CDN)
that may be configured to cache HTTP responses.

While HTTP caching is disabled by default on Cloudflare, you might activate this feature via
`page rules <https://support.cloudflare.com/hc/en-us/articles/218411427-Understanding-and-Configuring-Cloudflare-Page-Rules-Page-Rules-Tutorial->`_.
It is possible to enable caching per page, but the matching configuration is only
possible via *URL matching*, which doesn't allow you to disable the cache
when :ref:`Blackfire HTTP header <reverse-proxies-headers>` is present in the request.

The recommended solution is to use `Cloudflare workers <https://www.cloudflare.com/fr-fr/products/cloudflare-workers/>`_
**instead of page rules**. This solution is **free of charge until 100k
requests** going through the workers per day. Beyond that limit, Cloudflare
charges depending on the number of requests.

You can create a worker from your Cloudflare dashboard.

Worker Code
-----------

Once your worker is created, you will need to add the following JavaScript
code in the online editor:

.. code-block:: js

    addEventListener('fetch', event => {
        event.respondWith(handleRequest(event.request))
    })

    async function handleRequest(request) {
        const acl = [
            // Blackfire.io IPs
            // Ref https://docs.blackfire.io/reference-guide/faq#how-should-i-configure-my-firewall-to-let-blackfire-access-my-apps
            '46.51.168.2', '54.75.240.245'
            // Add your own IPs here, from which you'd like to disable the cache.
            // 'x.y.z.w'
        ]
        if (request.headers.get('x-blackfire-query') !== null && acl.includes(request.headers.get('cf-connecting-ip'))) {
            return fetch(request)
        }

        // Here, you may apply your own caching rule, the same you would have applied with page rules.
        return fetch(request, { cf: { cacheEverything: true } })
    }

Then click on the ``Save and Deploy`` button.

Worker Activation
-----------------

Now, activate your worker from your Cloudflare domain dashboard:

* Go to the *Workers* section and click on ``Add route``;
* Define your route (you will probably want to add everything, e.g. ``yourdomain.tld/*``);
* Choose your worker and click on ``Save``.

.. note::

    Please check that the ``cache everything`` setting is disabled from your
    page rules, as **the rules are applied after the workers**.
    They would hence override your workers' configuration.
