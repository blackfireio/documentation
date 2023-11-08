Doctrine DQL statements should be cached in production
======================================================

`Doctrine ORM`_ is the most popular ORM library used in PHP applications. Thanks
to this library, your applications can query SQL databases using the more convenient DQL language instead of raw SQL.

Transforming DQL statements into SQL is done automatically by Doctrine but is a heavy process.

Doctrine includes a cache mechanism to save the result of this processing, you
need to configure it. For instance, when using the Doctrine ORM inside a Symfony
application, add the following configuration to cache the DQL parsing:

.. code-block:: yaml

    # app/config/config_prod.yml
    doctrine:
        orm:
            query_cache_driver: apc

Read the `Doctrine configuration reference`_ to learn about all the cache types
supported by Doctrine.

.. _`Doctrine ORM`: https://www.doctrine-project.org/projects/orm.html
.. _`Doctrine configuration reference`: https://symfony.com/doc/current/reference/configuration/doctrine.html#caching-drivers
