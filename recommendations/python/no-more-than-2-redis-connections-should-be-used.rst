No More Than 2 Redis Connections Should Be Used
===============================================

`Redis`_  is a popular in-memory data store that is used as a database, a cache
and even a message broker. Before storing and fetching data from Redis,
applications must instantiate a client to connect to the Redis server.

Some applications may host different services (Redis, databases, web server, etc.)
on the same machine, but most of the time Redis is hosted on a different server.
Therefore, connecting to Redis introduces some overhead due to the TCP/IP
connection.

Blackfire detects the connections established with the library `redis-py`_. Unless
configured differently, you'll see this recommendation when establishing more
than two Redis connection during the application execution: one for the session
and one for the cache.

.. _`Redis`: https://redis.io
.. _`redis-py`:  https://github.com/andymccurdy/redis-py/
