"mbstring.func_overload" is not portable and should not be used
===============================================================

The `mbstring.func_overload`_ ini setting allows replacing some string related
functions with their counterparts from the `mbstring`_ extension.

Using this setting makes applications non-portable, and can introduce hard-to-
debug issues when used with third-party libraries that don't expect the string
functions to behave differently than the default ones.

For these reasons, the ``mbstring.func_overload`` setting has been deprecated in
PHP 7.2. and it's strongly recommended to disable it in your ``php.ini``
configuration using ``mbstring.func_overload=off`` (or by removing it, since
"off" is the default value).

.. _`mbstring.func_overload`: https://www.php.net/manual/en/mbstring.overload.php
.. _`mbstring`: https://www.php.net/manual/en/book.mbstring.php
