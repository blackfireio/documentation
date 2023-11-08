The Twig C extension should be installed
========================================

`Twig`_ is a popular template engine for PHP applications. Twig templates are
less verbose and more expressive than pure PHP templates. They are also secure
by default, which mitigates the risk of suffering from `XSS attacks`_.

Before rendering the contents, Twig templates are compiled to PHP code and the
result is cached for later reuse. Although the generated PHP code is heavily
optimized, the complex logic involved makes these templates execute a bit slower
than simple low-level PHP functions.

In order to minimize this overhead, Twig provides a PHP extension developed in
C programming language. This extension doesn't replace the entire PHP code, but
a subset of the most complex Twig features. Using this extension will boost your
application performance noticeably and for free.

First, build the Twig extension as any other PHP extension:

.. code-block:: bash

    $ cd <Twig-source-code-directory>
    $ cd ext/twig
    $ phpize
    $ ./configure
    $ make
    $ make install

Then, enable the extension in the ``php.ini`` configuration file of your PHP
engine and restart your server:

.. code-block:: ini

    extension=twig.so

Read `this chapter`_ in the Twig documentation for more information about this
extension and to learn how to install it on Windows systems.

.. _`Twig`: https://twig.symfony.com/
.. _`XSS attacks`: https://en.wikipedia.org/wiki/Cross-site_scripting
.. _`this chapter`: https://twig.symfony.com/doc/1.x/installation.html#installing-the-c-extension
