The Magento 1 collection cache should be enabled
================================================

It's regularly necessary to be able to access the data of an entity stored in
a database. While a model let you load one entity at once, Magento provides
objects called `collections` to let you load multiple entities at the same time.

This is especially useful when displaying a list, like the products associated
to a specific category. However, the large amount of data loaded by a collection
could quickly become a performance issue if the query is too wide or if the
results are retrieved too frequently.

In addition to the rendering cache (block HTML and full page cache), using the
collection cache can help to achieve best results in term of performance by
avoiding running the same queries several times on the database.

How To Enable this Cache
------------------------

Using the graphical interface, access the Magento **Admin Panel**, then click
on System > Cache Management and make sure that the **Collections Data ** status
is **Enabled**.
