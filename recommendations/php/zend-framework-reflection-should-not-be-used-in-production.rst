Zend Framework Reflection should not be used in production
==========================================================

`Zend Server Reflection`_ provides a standard mechanism to introspect PHP
classes and functions. It's based on PHP 5 `Reflection API`_ but it adds utility
methods to retrieve descriptions (for parameters, return values and
function/methods) and to get the full list of function/method prototypes.

Introspecting this information during runtime can slow down the application
execution. That's why Blackfire alerts you whenever the
``Zend\\Server\\Reflection`` or ``Zend_Server_Reflection`` classes are used.

The alternative to using Zend Server Reflection is to introspect the information
once and cache the result.

.. _`Zend Server Reflection`: https://framework.zend.com/manual/current/en/modules/zend.server.reflection.html
.. _`Reflection API`: https://www.php.net/manual/en/book.reflection.php
