The Composer autoloader class map should be dumped in production
================================================================

`Composer`_ is the de-facto dependency management tool for PHP; it allows
developers to declare the libraries the projects depend on and manages them
automatically (install/update).

Composer also manages class `autoloading`_ by generating an autoloader class in
``vendor/autoload.php`` when ``composer install``, ``composer update``, or
``composer dump-autoload`` is run. For instance, to automatically autoload all
classes of the ``Acme\`` namespace stored under the ``src/`` directory, add the
following snippet to the project's ``composer.json`` file:

.. code-block:: json

    {
        "autoload": {
            "psr-4": {"Acme\\": "src/"}
        }
    }

Whenever PHP loads a class, Composer has to look for the corresponding file on
the filesystem which is a slow process. But this can be optimized for
production as the directory structure should never change.

Using ``composer dump-autoload --optimize`` tells Composer to dump an optimized
version of the autoloader by generating a **classmap**. Because the classmap
can be huge, it's highly recommended to have a PHP opcode cache installed (like
Zend OPcache).

.. _Composer: https://getcomposer.org/
.. _autoloading: https://getcomposer.org/doc/01-basic-usage.md#autoloading
