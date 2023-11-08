Less server-side HTTP calls should be made
==========================================

Modern web applications increasingly make use of third-party services via APIs.
For that reason, rendering a single page may require performing several HTTP
round-trips to the server.

HTTP calls are slow by nature because they require establishing a connection,
transferring data and dealing with the TCP/IP protocol overhead and the network
conditions.

.. note::

    The new `HTTP/2`_ protocol improves HTTP/1 performance significantly thanks
    to multiplexing and pipelining requests, compressing headers, etc. However,
    it's still recommended to not perform too many HTTP/2 calls.

In order to reduce the number of HTTP requests, make use of a caching mechanism.
If not possible, try to combine multiple requests into a single one that returns
more information, perform several HTTP calls in parallel, etc.

.. _`HTTP/2`: https://en.wikipedia.org/wiki/HTTP/2
