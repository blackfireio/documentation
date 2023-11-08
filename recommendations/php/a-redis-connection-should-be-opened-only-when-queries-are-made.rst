A Redis connection should be opened only when queries are made
==============================================================

The `Redis Protocol specification`_ describes in the networking layer section
how clients connect to Redis servers creating TCP connections to the port 6379
(or using equivalent stream-oriented connections like Unix sockets).

Therefore, connecting to the Redis server introduces some overhead due to the
TCP/IP connection. If your application is not performing any Redis queries, you
should not connect to the Redis server.

.. _`Redis Protocol specification`: https://redis.io/topics/protocol
