"magic_quotes_gpc" is deprecated and should be turned off
=========================================================

The `magic_quotes_gpc`_ ini setting was deprecated in PHP 5.3 and removed in PHP
5.4. When enabled, PHP "magically" escapes singles quotes, double quotes and
``null`` values found in the variables related to GET, POST and Cookie
operations. To make matter worse, another setting called ``magic_quotes_sybase``
can alter the already magic behavior of ``magic_quotes_gpc``.

This feature was designed to help beginners avoid SQL injections by
automatically escaping the information. Nowadays, developers are aware of these
security issues and use parameter binding instead of argument escaping.

You should disable this setting using ``magic_quotes_gpc=Off`` in your ``php.ini``
configuration for various reasons:

* your applications will be more portable because their behavior does not depend
  on a ini setting;
* the application performance will improve because data escaping would only be
  done when needed;
* your applications don't need escaping all the time; it's not convenient to
  manipulate only escaped content.

.. _`magic_quotes_gpc`: https://www.php.net/manual/en/info.configuration.php#ini.magic-quotes-gpc
.. _`magic_quotes_sybase`: https://www.php.net/manual/en/sybase.configuration.php#ini.magic-quotes-sybase
