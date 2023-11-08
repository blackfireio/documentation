You should execute less SQL queries in Magento 2
================================================

Magento 2 stores most of its data in relational databases such as MySQL or
MariaDB. It performs many SQL queries to fetch the information needed to
render the contents displayed to the end users.

The vast majority of SQL queries are very fast when executing them in the
database server. However, each SQL query introduces some overhead in your
application. Magento performs queries mostly synchronously, so each time a
query is sent to the database, your PHP code stops executing and just waits
for a result.

Reducing the Number of SQL Queries
----------------------------------

In Magento, too many queries is usually a symptom of one of the following other
issues:

* :doc:`Reduce the number of product loads </recommendations/php/you-should-not-load-a-product-directly-on-magento-2>`
* :doc:`Activate the Block HTML Cache </recommendations/php/the-magento-2-block-html-cache-should-be-enabled>`
* :doc:`Reduce the number of entity loads </recommendations/php/you-should-load-less-entities-on-a-magento-2-homepage>`

There are also some :doc:`generic techniques </recommendations/php/you-should-execute-less-sql-queries>` you could try.

