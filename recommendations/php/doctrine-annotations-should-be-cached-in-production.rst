Doctrine annotations should be cached in production
===================================================

`Doctrine ORM`_ is the most popular ORM library used in PHP applications. Thanks
to this library, your applications can manipulate the information stored in the
database using PHP objects instead of SQL statements.

Before using the ORM, you must create those PHP objects and define some
configuration to help Doctrine transform the objects into database records. This
configuration is called "entity mapping" and can be defined in different formats
(XML, YAML, PHP).

Lots of applications define the entity mapping using PHP annotations, because
they are very convenient. In this example, the ``Book`` PHP class includes
annotations to define the database table and columns where the information is
stored:

.. code-block:: php

    // src/Acme/Entity/Book.php
    namespace Acme\Entity;

    use Doctrine\ORM\Mapping as ORM;

    /**
     * @ORM\Entity
     * @ORM\Table(name="acme_book")
     */
    class Book
    {
        /**
         * @ORM\Column(type="string", length=255)
         */
        private $title;

        // ...
    }

However, using annotations for mapping comes at a cost: Doctrine must transform
that configuration into the regular PHP code executed by the application. In
real applications with lots of complex entities, this conversion process
severely impacts the performance. That's why you should cache Doctrine
annotations parsing in production.

Doctrine already includes a cache mechanism, so you need to configure it. For
instance, when using the Doctrine ORM inside a Symfony application, add the
following configuration to cache the annotations parsing:

.. code-block:: yaml

    # app/config/config_prod.yml
    doctrine:
        orm:
            metadata_cache_driver: apc

Read the `Doctrine configuration reference`_ to learn about all the cache types
supported by Doctrine.

.. _`Doctrine ORM`: https://www.doctrine-project.org/projects/orm.html
.. _`Doctrine configuration reference`: https://symfony.com/doc/current/reference/configuration/doctrine.html#caching-drivers
