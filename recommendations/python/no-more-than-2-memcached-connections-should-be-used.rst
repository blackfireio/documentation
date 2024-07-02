No More Than 2 Memcached Connections Should Be Used
===================================================

`memcached`_  is a popular high-performance, distributed memory object caching
system. Before storing and fetching data from memcache, applications must
instantiate a client to connect to the Memcached server.

Some applications may host different services (memcached, databases, web server, etc.)
on the same machine, but most of the time ``memcached`` is hosted on a different server.
Therefore, connecting to memcached introduces some overhead due to the TCP/IP
connection.

Blackfire detects the connections established with the most popular Python libraries
for ``memcached``, such as `pymemcache`_ , `pylibmc`_ and `python-memcached`_. Unless
configured differently, you'll see this recommendation when establishing more
than two Memcached connection during the application execution: one for the session
and one for the cache.

.. _`memcached`: https://memcached.org/
.. _`pymemcache`: https://github.com/pinterest/pymemcache/
.. _`pylibmc`: https://github.com/lericson/pylibmc
.. _`python-memcached`: https://github.com/linsomniac/python-memcached
