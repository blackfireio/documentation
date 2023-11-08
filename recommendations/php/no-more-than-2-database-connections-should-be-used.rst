No more than 2 database connections should be used
==================================================

Most dynamic applications make use of databases to store their information.
Before storing and fetching data, applications must instantiate a client to
connect to those database servers.

Simple applications host different services (message brokers, databases, web
server, etc.) on the same machine, but most of the times databases are hosted
on a different server. Therefore, connecting to the database server introduces
some overhead due to the TCP/IP connection.

Using two different databases is a common scenario for lots of web applications:
one database to read data and the other to write it; one database to read/write
data and the other to store sessions; etc.

Blackfire detects the connections established with any of the database types
supported by PHP. Unless configured differently, you'll see this recommendation
when establishing more than two database connections during the application
execution.
