Shell commands should not be spawned during a Web request
=========================================================

The `program execution functions`_ provided by Python should be avoided by most
web applications. They are slow because they have to fork a new process and
read a new executable file, including its dependent libraries. They often also
have to spawn a shell to parse the command line, making them even slower.

These functions might also lead to arbitrary code execution, if the parameters
are not sanitized well and consist malicious user input.

You should prefer implementing the functionality you need in Python. If you have
to communicate with an external program, prefer network communication.

If you must use an external program, and its results don't often change, you
should cache them.

.. _`program execution functions`: https://docs.python.org/3/library/subprocess.html
