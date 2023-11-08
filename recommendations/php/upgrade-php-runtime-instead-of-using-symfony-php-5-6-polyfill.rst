Upgrade PHP runtime instead of using Symfony PHP 5.6 polyfill
=============================================================

`Symfony polyfills`_ provide pure PHP implementations of some PHP extensions and
functions. They allow for example to use some PHP 7.x functions in PHP 5.x
applications or use *mbstring* functions even when that PHP extension is not
enabled.

These polyfills help developers create portable applications that work even when
some requirements, like ``mbstring`` or ``iconv``, are missing on the servers
where they are deployed.

However, the PHP implementations are much slower than the native implementations
provided by PHP, which are written in C. Moreover, as the polyfills are based
upon the original implementation, sometimes they are incomplete or behave
differently in edge-cases.

This is why you should not use them, neither in production nor in development.
Instead, install the appropriate PHP version or extensions required by the
application.

.. _`Symfony polyfills`: https://github.com/symfony/polyfill/
