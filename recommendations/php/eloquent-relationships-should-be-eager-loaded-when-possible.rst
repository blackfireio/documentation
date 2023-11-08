Eloquent relationships should be eager loaded when possible
===========================================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by dflydev`_.

When using related models with Eloquent, there are two ways for Eloquent to
load the related model from the database.

The default behavior is for these related models to be loaded on-demand. This
is also known as "lazy loading". When a related model is requested from
a hydrated model, Eloquent queries the related model right then
and there.

While lazy loading is quite convenient for the developer, it can come at a high
cost to performance. This is best illustrated with the N+1 problem.

To illustrate the N+1 problem, consider an ``Article`` object that is
related to many ``Comment`` objects. Lazy loading would result in 1
query to retrieve the ``Article`` plus 1 query to retrieve the
``Comment`` objects for that ``Article``. This results in 2
queries total. This is the best-case scenario for N + 1
where N is equal to 1.

.. code-block:: php

    use App\Models\Article;

    $article = Article::find(7);

    foreach ($article->comments as $comment) {
        echo $comment->title;
    }

Where N+1 becomes a larger issue is when multiple ``Article`` objects are
possible. While all ``Article`` instances may still be retrieved using
just 1 query, there will need to be 1 query **per** ``Article`` to
find the ``Comment`` objects for **each** ``Article``.

So, if there are 200 ``Article`` instances returned from the first query,
an additional **200 queries** will be executed to find the ``Comment``
instances for **each** of those 200 ``Article`` instances.

.. code-block:: php

    use App\Models\Article;

    $articles = Article::published()->get();

    foreach ($articles as $article) {
        foreach ($article->comments as $comment) {
            echo $comment->title;
        }
    }

The N+1 problem only gets worse the deeper the relationship tree gets.
Consider if our example extended the ``Comment`` model to be related
to one ``Author`` instance. Now, consider also that a single
``Author`` instance may be related to zero or more
``Comment`` instances, each of which is related
to an ``Author`` instance.

.. code-block:: php

    use App\Models\Article;

    $articles = Article::published()->get();

    foreach ($articles as $article) {
        foreach ($article->comments as $comment) {
            echo $comment->author->name;
        }
    }

If there are 100 ``Article`` instances and each has 100 ``Comment`` instances,
the above code would result in 10,101 queries!

 * 1 query to retrieve the ``Article`` instances
 * 100 queries to retrieve the ``Comment`` instances for each ``Article``
 * 10,000 queries to retrieve the ``Author`` instances for each ``Comment``

It's not hard to see how this could quickly spin out of control.

Eager loading relationships
---------------------------

Fortunately, Eloquent provides a way to address the N+1 problem. Instead of
using the default lazy loading behavior, Eloquent can be instructed to use
`eager loading`_ instead.

Eager loading queries and builds related models together at one time rather
than doing them on demand.

This is how eager loading can be used for the example above:

.. code-block:: php

    use App\Models\Article;

    $articles = Article::published()->with('comments.author')->get()

    foreach ($articles as $article) {
        foreach ($article->comments as $comment) {
            echo $comment->author->name;
        }
    }

The ``->with()`` call instructs Eloquent to eager load some relationships
on ``Article`` when the query is executed. This means the related
models will already be hydrated when they are accessed later.

By specifying the relationships to eager load in this example, Eloquent will
only execute 3 queries total. This will be the case regardless of the
number of ``Article`` instances, ``Comment`` instances per
``Article``, and number of ``Author`` instances.

.. _`a contribution by dflydev`: https://dflydev.com/
.. _`eager loading`: https://laravel.com/docs/8.x/eloquent-relationships#eager-loading
