No more than 2 MongoDB connections should be used
=================================================

`MongoDB`_ is a popular document-oriented database used by applications that
don't rely on the traditional relational database structure. Before storing and
fetching data, applications must instantiate a client to connect to the MongoDB
server.

Simple applications host different services (MongoDB, databases, web server,
etc.) on the same machine, but most of the times MongoDB is hosted on a
different server. Therefore, connecting to the MongoDB server introduces some
overhead due to the TCP/IP connection.

Using two different databases is a common scenario for lots of web applications:
one database to read data and the other to write it; one database to read/write
data and the other to store sessions; etc.

Blackfire detects the connections established with the official MongoDB PHP
extension. Unless configured differently, you'll see this recommendation
when establishing more than two MongoDB connections during the application
execution.

.. _`MongoDB`: https://en.wikipedia.org/wiki/MongoDB
