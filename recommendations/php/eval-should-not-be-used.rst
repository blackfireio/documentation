eval() should not be used
=========================

The `eval() function`_ takes the given string argument and executes it as if
it were PHP code, returning the result of the execution. It's strongly
recommended to not use this function because of these reasons:

* It may introduce security issues when the evaluated content depends on
  information provided by the end users.
* It hurts the application performance because the code inside ``eval()`` must
  be compiled dynamically at runtime and cannot use the PHP OPcache. This is
  specially important for PHP 7 applications, because compilation makes more
  optimizations than in PHP 5 and therefore is slower.
* It hurts productivity because it's harder to learn how the application works,
  and it takes more time to debug issues in the evaluated code.

Generally speaking, the only valid use case for the ``eval()`` function is to
evaluate complex mathematic expressions.

.. _`eval() function`: https://www.php.net/eval
