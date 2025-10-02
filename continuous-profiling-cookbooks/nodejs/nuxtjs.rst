Nuxt [level: Production]
========================

`NuxtJS <https://nuxt.com/>`_ is an open-source framework built on top of
`Vue.js <https://vuejs.org/>`_ that simplifies building modern, performant web
applications with server-side rendering, static site generation, and a powerful
module ecosystem.

Requirements
------------

- Node.js >= 22.0.0+
- NuxtJS >= 3.0+
- :doc:`Blackfire Agent </up-and-running/configuration/agent>` >= 2.13.0

Installation
------------

Install the Blackfire Node.js tracing library:

.. code-block:: bash
    :zerocopy:

    npm install @blackfireio/node-tracing

Configuration
-------------

Create a new plugin in your NuxtJS project: ``./server/plugins/blackfire.ts``

.. code-block:: js
    :zerocopy:

    // server/plugins/blackfire.ts
    export default defineNitroPlugin(async () => {
    if (process.env.BLACKFIRE_ENABLE !== '1') return;

    try {
        // Works in ESM: dynamically import and handle both default/named exports
        const mod = await import('@blackfireio/node-tracing');
        const Blackfire: any = (mod as any).default || mod;

        Blackfire.start({
        appName:
            process.env.BLACKFIRE_APP_NAME || 'shopware-frontend',
        // durationMillis: 45000,
        // cpuProfileRate: 100,
        // labels: { service: 'frontend', framework: 'nuxt3' },
        });

        console.info('[blackfire] node-tracing started');
    } catch (e) {
        console.error('[blackfire] failed to start node-tracing', e);
    }
    });

Configuration
~~~~~~~~~~~~~

Add the following environment variable to control the continuous profiling:
``BLACKFIRE_ENABLE=1``.

Check the :doc:`Node.js Continuous Profiling reference <./configuration>`
for all the configuration options.
