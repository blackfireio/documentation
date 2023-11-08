Neither "die()" nor "exit()" should be used during Web requests
===============================================================

PHP functions ``exit()`` and ``die()`` completely stop the execution flow of a PHP program.

Generally speaking, the best practice is to use (typed) `Exceptions`_ to interrupt the execution flow.
Exceptions are explicit, can be caught, and carry enough information to help debugging.
On the other hand, ``exit()`` and ``die()`` are completely silent and offer no clue to the developer
about the reason why the execution ended.

In the Symfony context, using ``exit()`` or ``die()`` means that tasks executed at the end
of a request (like closing database connections or flushing logs to file) never get executed.
Therefore, you may put your application in an unstable state for the next queries.

Sometimes, developers need to stop the execution of a Symfony request in order to speed up the
debugging process. This is a perfect use case for unit tests: instead of debugging a PHP method
via a Symfony request with a die(), write a unit test for this method.
It will execute extremely fast - as long as your code is decoupled enough.

.. _`Exceptions`: https://www.php.net/manual/en/language.exceptions.php
