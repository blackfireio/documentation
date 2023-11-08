PHP Preloading should be configured
===================================

`PHP Preloading`_ is a feature which has been introduced into PHP 7.4.0 and
allows to *preload* scripts into the opcache. This mechanism makes it
possible to keep specific symbols (functions, classes, etc) available across
requests, without the need to be explicitly included.

Preloading is part of the `OPcache extension`_ and needs to be configured
through the ``opcache.preload`` INI directive. The value of this setting must
be an absolute path to the preloading script.

Symfony
-------

Symfony provides a preload script out-of-the-box as of version 4.4.
The absolute path to this script can be directly specified in the ``opcache.preload``
directive:

.. code-block:: ini

    ; as of Symfony 4.4.14 or 5.1.6
    opcache.preload=/app/config/preload.php

    ; on Symfony 5.1+ before 5.1.6
    opcache.preload=/app/var/cache/prod/App_KernelProdContainer.preload.php

    ; for Symfony 4.4 before 4.4.14
    opcache.preload=/app/var/cache/prod/srcApp_KernelProdContainer.preload.php

Laravel
-------

The `Laraload package`_ can be used to generate a preload script for your Laravel app.

Other Frameworks
----------------

The `OPcache Preloader library`_ can be used to help you generate a preload script.
It leverages OPcache statistics to figure out which files / classes are the most used
in your application, in order to add them to the preload script.

.. _`PHP Preloading`: https://www.php.net/manual/en/opcache.preloading.php

.. _`OPcache extension`: https://www.php.net/manual/en/book.opcache.php

.. _`Laraload package`: https://github.com/DarkGhostHunter/Laraload

.. _`OPcache Preloader library`: https://github.com/DarkGhostHunter/Preloader
