Twig template cache should be enabled in production
===================================================

`Twig`_ is a popular template engine for PHP applications. Twig templates are
less verbose and more expressive than pure PHP templates. They are also secure
by default, which mitigates the risk of suffering `XSS attacks`_.

Before using the Twig templates to render contents, they must be transformed
into regular PHP code. This process is known as "template compilation" and it's
designed to create the most optimized PHP code possible.

Given its complexity, the compilation phase takes a non-negligible time to
complete and has a negative impact on your application performance. Twig
provides a feature to compile the templates once and cache the result to reuse
it whenever the template is rendered.

Twig cache should always be enabled when running the application on production.
If you use Twig as a stand-alone library, enable the cache with the ``cache``
option of the ``Twig_Environment`` class:

.. code-block:: php

    require_once '/path/to/lib/Twig/Autoloader.php';
    Twig_Autoloader::register();

    $loader = new Twig_Loader_Filesystem('/path/to/templates');
    $twig = new Twig_Environment($loader, array(
        'cache' => '/path/to/compilation_cache',
    ));

If you use Twig as part of an application (e.g. Drupal) or a framework (e.g.
Symfony) make sure that the Twig cache is enabled.

.. _`Twig`: https://twig.symfony.com/
.. _`XSS attacks`: https://en.wikipedia.org/wiki/Cross-site_scripting
