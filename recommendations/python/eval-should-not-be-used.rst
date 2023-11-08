eval() should not be used
=========================

The `eval() function`_ takes the given string argument and executes it as if
it were Python code, returning the result of the execution. It's recommended
to not use this function because of these reasons:

* It may introduce security issues when the evaluated content depends on
  information provided by the end users.
* It hurts the application performance because the code inside ``eval()`` must
  be compiled dynamically at runtime.
* It hurts productivity because it's harder to learn how the application works,
  and it takes more time to debug issues in the evaluated code.

.. _`eval() function`: https://docs.python.org/3/library/functions.html#eval
