No More Than 2 Database Connections Should Be Used
==================================================

Most dynamic applications use databases to store their information.
Before storing and fetching data, applications must instantiate a client to
connect to the database server.

Small applications host different services (message brokers, databases, web
server, etc.) on the same machine, but most of the time databases are hosted
on a different server. Therefore, connecting to the database server introduces
some overhead due to the TCP/IP connection.

Using two different databases is a common scenario for lots of web applications, e.g.:

- one database to read data and the other to write it;

- one database to read/write data and the other to store sessions;

- etc.

In order to avoid too much overhead due to the Database connection, it is
advised to keep the number of connections as low as possible, ideally no more
than 2 for the same request.
