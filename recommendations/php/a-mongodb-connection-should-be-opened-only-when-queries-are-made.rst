A MongoDB connection should be opened only when queries are made
================================================================

The `MongoDB Wire Protocol`_ describes how clients connect to the MongoDB server
using regular TCP/IP sockets without performing a connection handshake. Therefore,
the overhead introduced by connections is much lower than in other comparable
technologies.

However, given that the connection overhead is not null, your application should
not connect to the MongoDB server unless it's going to perform some queries.

.. _`MongoDB Wire Protocol`: https://docs.mongodb.com/manual/reference/mongodb-wire-protocol/
