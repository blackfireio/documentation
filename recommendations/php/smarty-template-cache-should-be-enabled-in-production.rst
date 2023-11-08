Smarty template cache should be enabled in production
=====================================================

`Smarty`_ is a template engine for PHP applications. Before using the Smarty
templates to render contents, they must be transformed into regular PHP code.
This process is known as "template compilation" and it's designed to create the
most optimized PHP code possible.

Given its complexity, the compilation phase takes a non-negligible time to
complete and has a negative impact on your application performance. Smarty
provides a feature to compile the templates once and cache the result to reuse
it whenever the template is rendered.

.. code-block:: php

    require('Smarty.class.php');

    $smarty = new Smarty();
    // enable the template caching
    $smarty->caching = 1;
    // default cache lifetime is 3600 (1 hour)
    $smarty->cache_lifetime = 600;

    $smarty->display('...');

Smarty defines another option called ``compile_check``. If set to ``true``,
Smarty checks the modification time of every template and config file that is
involved with the cached template. If any of those files is modified, the
template is recompiled automatically. In production environment, set this option
to ``false`` because templates will never change:

.. code-block:: php

    // ...

    // don't check whether templates have changed since compilation
    $smarty->compile_check = false;

.. _`Smarty`: https://www.smarty.net
