You should not use XDebug in production
=======================================

While developing an application, you may want to use `Xdebug`_'s functions
to understand what happens at runtime and for troubleshooting,
but developers must not forget to remove such debug statements before committing the code.

Moreover, the overhead introduced by Xdebug `skews the performance numbers`_
and it can make you optimize the wrong parts of your application.

.. _`Xdebug`: https://xdebug.org
.. _`skews the performance numbers`: https://nikic.github.io/2012/01/19/Careful-XDebug-can-skew-your-performance-numbers.html
