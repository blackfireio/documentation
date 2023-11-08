You should execute less SQL queries
===================================

Relational databases are one of the most popular ways to store information for
web applications. Consequently, it's common to perform some SQL queries to fetch
the information needed to render the contents displayed to the end users.

The vast majority of SQL queries are very fast when executing them in the
database server. However, each SQL query introduces some overhead in your
application:

* If the database is located on a separate server, you must take into account
  the round-trip communication needed to send the query and get the results;
* If the database server is under heavy-load, the query execution must wait
  until the server frees some of its resources;
* If your application uses a database abstraction library, such as an ORM, the
  original query must be parsed to get the real SQL query executed and the
  results must be processed to turn them into the structure required by the
  application.

These are some of the reasons why you should not execute too many SQL queries to
generate your contents.

Reducing the Number of SQL Queries
----------------------------------

There is no "silver bullet" to solve this problem, but there are some generic
techniques which can help you reduce the number of SQL queries in your
applications.

First, avoid making SQL queries in loops without being aware of it. This happens
for example when using an ORM which lazy loads the related entities:

.. code-block:: jinja

    {% for book in books %}
        {{ book.author.name }}
    {% endfor %}

In this example, the application could end up making one SQL query for each loop
iteration to get the information of the author. This is called the "N+1 query
problem" and it's by far the most common cause for executing too many queries.

The simplest solution to the N+1 problem is to "eager load" the related entities.
In other words, in the above example we'd execute one query to get the books and
then another query to get all the authors for the books returned in the first
query.

In applications that use Django, use the ``select_related`` method to define the
relationships that must be loaded eagerly:

.. code-block:: python

   books = Books.objects.select_related('author').all()
