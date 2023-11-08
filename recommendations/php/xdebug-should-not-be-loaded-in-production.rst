XDebug should not be loaded in production
=========================================

`Xdebug`_ is a popular tool used to debug PHP applications. Xdebug requires to
install and enable a PHP extension that hooks into your application. Despite its
usefulness, just loading Xdebug introduces massive performance penalties,
even if you don't use it actively. That's why you should always disable it
on your production servers.

Moreover, the overhead introduced by Xdebug `skews the performance numbers`_
and it can make you optimize the wrong parts of your application.

.. _`Xdebug`: https://xdebug.org
.. _`skews the performance numbers`: https://nikic.github.io/2012/01/19/Careful-XDebug-can-skew-your-performance-numbers.html
