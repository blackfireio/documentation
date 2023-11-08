Doctrine proxies should be cached in production
===============================================

From Doctrine documentation about `proxy objects`_:

    Doctrine generates classes that extend your entity classes and adds
    lazy-loading capabilities to them. Doctrine can then give you an
    instance of such a proxy class whenever you request an object of the
    class being proxied.

Generating proxies is a CPU intensive process that should not happen while your
application is running. Instead, it should be done before the application is
deployed, typically using a dedicated command line.

In a typical Symfony application, on prod, you should disable the
``auto_generate_proxy_classes`` setting of the `Doctrine bundle`_:

.. code-block:: yaml

    # app/config/config_prod.yml
    doctrine:
        orm:
            auto_generate_proxy_classes: false

.. _`proxy objects`: https://www.doctrine-project.org/projects/doctrine-orm/en/latest/reference/advanced-configuration.html#title.1.4
.. _`Doctrine bundle`: https://symfony.com/doc/current/reference/configuration/doctrine.html
