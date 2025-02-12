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

- Using Data Transfer Objects (DTOs);

- Using ``JOIN`` clauses to add extra fields to the query;

- Using regular SQL queries in batch processing instead of the ORM whenever possible,
  as they are usually more efficient, especially when the Entity class and its
  logic are not needed.

Examples with Doctrine ORM
--------------------------

- Use the `EXTRA_LAZY association`_, to avoid the full load of the related collections.
  This can be specifically useful when using methods such as ``count`` or
  ``contains`` (full list of supported methods on `EXTRA_LAZY association`_
  documentation.

- Use `HYDRATE_ARRAY hydration mode`_ when applicable. This avoids the creation of
  of entity objects when their logic is not needed.

- Use `DTOs with the NEW operator`_, instead of requesting a whole entity.

- Add extra fields to your query using ``JOIN`` clauses:

.. code-block:: php

    use Doctrine\Bundle\DoctrineBundle\Repository\ServiceEntityRepository;
    use Doctrine\ORM\QueryBuilder;

    class ArticleRepository extends ServiceEntityRepository
    {
        public function findLatestQueryBuilder(int $maxResults): QueryBuilder
        {
            return $this->createQueryBuilder('article')
                // Join the related comments, grouped by article and add an additional
                // field containing the comments count.
                ->leftJoin('article.comments', 'comments')
                ->groupBy('article.id')
                ->addSelect('COUNT(comments.id) as commentsCount')
                ->setMaxResults($maxResults)
                ->orderBy('article.createdAt', 'DESC');
        }

.. code-block:: jinja

    {# Each row is an array containing the entity itself at index 0. #}
    {# The additional fields are indexed by their alias in the query. #}
    {% for articleData in articles %}
        {% set article = articleData.0 %}
        {% set commentsCount = articleData.comments_count %}

        {# ... #}
            {{ articleData.title }}

            {{ commentsCount }}
        {# ... #}
    {% endfor %}

.. _`EXTRA_LAZY association`: https://www.doctrine-project.org/projects/doctrine-orm/en/latest/tutorials/extra-lazy-associations.html
.. _`HYDRATE_ARRAY hydration mode`: https://www.doctrine-project.org/projects/doctrine1/en/latest/manual/data-hydrators.html#array
.. _`Object Relation Mapper`: https://en.wikipedia.org/wiki/Object-relational_mapping
.. _`DTOs with the NEW operator`: https://www.doctrine-project.org/projects/doctrine-orm/en/latest/reference/dql-doctrine-query-language.html#new-operator-syntax
