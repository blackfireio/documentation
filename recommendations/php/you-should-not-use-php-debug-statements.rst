You should not use PHP debug statements
=======================================

While developing an application, it's common to add debug statements like ``print_r()``, ``var_export`` or ``var_dump()``.
It can be convenient to understand what happens at runtime and for troubleshooting,
but developers must not forget to remove such debug statements before committing the code.

Instead of sprinkling debug statements throughout your codebase, consider
injecting a logger into your services as a general rule. Sending debug messages
to the logger is a good practice, and you can filter or scan your logs for a
particular channel using ``grep``.
