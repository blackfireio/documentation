You should execute less SQL queries in Sylius
=============================================

Sylius stores most of its data into relational databases such as MySQL or
MariaDB. It performs many SQL queries to fetch the information needed to
render the contents, to be displayed to the end users.

The vast majority of SQL queries are very fast when executing them on the
database server. However, each SQL query introduces some overhead in your
application. Sylius performs queries mostly synchronously, so each time a
query is sent to the database, your application pauses and waits
for the result.

It also uses Doctrine ORM. Thanks to this library, your applications can
manipulate the information stored in the database using PHP objects instead
of SQL statements.

Reducing the Number of SQL Queries
----------------------------------

There are some :doc:`generic techniques </recommendations/php/you-should-execute-less-sql-queries>` you could try.
