Configuring Blackfire Continuous Profiler for Node.js [level: Production]
=========================================================================

The Node.js continuous profiling is currently made across 2 dimensions:

- **wall-time**: elapsed time per function call

- **heap**: memory allocation and reserved space over time

Requirements
------------

- Node.js >= 16.0.0

- Blackfire Agent >= 2.13.0

Installation
------------

Get the `Blackfire Continuous Profiler Node.js library <https://github.com/blackfireio/node-continuous-profiling>`_:

.. code-block:: bash

    npm install @blackfireio/node-tracing

Node.js continuous profiler API
________________________________

The Node.js continuous profiler API has two functions:

.. code-block:: js

    function start(config) {}
    function stop() {}


``function start(config) {}``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The ``start`` function starts the continuous profiler probe.
It collects profiling information in the background and periodically uploads it
to the Blackfire Agent until the ``stop`` function is called.


.. code-block:: js

    const Blackfire = require('@blackfireio/node-tracing');

    Blackfire.start({
        appName: 'my-app'
    });

    // your application...
    // If needed, you can stop profiling before cpuDuration
    // Blackfire.stop();


The ``Start`` function accepts an object as a parameter with the following keys:

- ``appName``: name of the application

- ``durationMillis``: time in milliseconds for which to collect profile (default: 45_000)

- ``cpuProfileRate``: average sampling frequency in Hz. (default: 100)

- ``labels``: Labels to add to the profile. (default: {})

- ``uploadTimeoutMillis``: Timeout in milliseconds for the upload request (default: 10000)


``function stop() {}``
~~~~~~~~~~~~~~~~

Stops the continuous profiling probe.


A simple example application
_____________________________

1/ Get the Blackfire Continuous Profiler Node.js library:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

    npm install express @blackfireio/node-tracing

2/ Create `index.js` with the following code:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: js

    const Blackfire = require('@blackfireio/node-tracing');
    const express = require('express')
    const crypto = require("crypto");
    const app = express()
    const port = 3000

    app.get('/', (req, res) => {
        const salt = crypto.randomBytes(128).toString("base64");
        const hash = crypto.pbkdf2Sync("this is my password", salt, 10000, 512, "sha512");

        res.send('Hello World!');
    })


    app.listen(port, () => {
        console.log(`Example app listening on port ${port}`)
        Blackfire.start({appName: 'blackfire-example'});
    })

3/ Run the Node.js server:
~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block::

    node index.js
