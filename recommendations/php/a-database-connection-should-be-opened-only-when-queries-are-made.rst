A database connection should be opened only when queries are made
=================================================================

Connecting to a database server usually requires establishing a TCP connection
or using an equivalent stream-oriented connections like Unix sockets.

Therefore, connecting to the database server introduces some overhead due to the
TCP/IP connection. If your application is not performing any SQL queries, you
should not connect to the database server.
