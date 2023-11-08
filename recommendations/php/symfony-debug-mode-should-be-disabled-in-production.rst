Symfony debug mode should be disabled in production
===================================================

In Symfony applications, a *kernel class* is responsible of handling the
incoming requests to produce the appropriate responses. Kernel classes extend
from the base `Kernel class`_ provided by Symfony.

The constructor of the base kernel class defines a second boolean argument
called ``$debug``. If this argument is set to ``true``, the kernel enables the
debug features of Symfony. Although debugging is useful when developing the
application, it introduces a significant impact in the application performance.
That's why the Symfony Kernel debug should be disabled in production.

.. _`Kernel class`: https://api.symfony.com/master/Symfony/Component/HttpKernel/Kernel.html
