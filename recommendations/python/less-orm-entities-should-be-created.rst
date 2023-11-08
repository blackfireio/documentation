Less ORM Entities Should Be Created
===================================

When using an `Object Relation Mapper`_ (ORM) to manage data with a relational
database, an object called "Entity" is created for each entry extracted from the
requests made to the database. This usually include result entries from the
configured relationships (``1-many``, ``1-1``, ``many-many``).

In some cases, **a few SQL queries can result in the creation of many entities**.
A typical example is the load of ``Article`` objects, triggering the load of many
related ``Comment`` objects.

Creating and Hydrating (i.e. filling up with data) entities is a heavy process,
and should therefore be controlled to avoid performance and memory issues.
As such, you may consider:

- Avoiding the creation of entities when you only need metadata such as
  the number of relations. Use ``COUNT`` instead;

- Not using the entity creation process, unless you really need it;

- Using ``JOIN`` clauses to add extra fields to the query;

- Using regular SQL queries in batch processing instead of the ORM whenever possible,
  as they are usually more efficient, especially when the Entity class and its
  logic are not needed.

.. _`Object Relation Mapper`: https://en.wikipedia.org/wiki/Object-relational_mapping
