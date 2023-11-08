Shell commands should not be spawned during a Web request
=========================================================

The `program execution functions`_ provided by PHP should be avoided by most
web applications. They are slow because they have to fork a new process and
read a new executable file, including its dependent libraries. They often also
have to spawn a shell to parse the command line, making them even slower.

These functions also have security issues, you should never pass them
parameters that depend upon user input.

You should prefer implementing the functionality you need in PHP. If you have
to communicate with an external program, prefer network communication. For
example, use the `MySQL extension`_ instead of spawning the ``mysql``
command-line program.

If you must use an external program, and its results don't often change, you
should cache them.

.. _`program execution functions`: https://www.php.net/manual/en/book.exec.php
.. _`MySQL extension`: https://www.php.net/manual/en/book.mysqli.php
