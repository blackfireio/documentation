Setting Shell Flag To True In Subprocess Functions Should Be Avoided
====================================================================

Calling `Subprocess functions`_ ``subprocess.run``, ``subprocess.call`` or
``subprocess.Popen`` with ``Shell=True`` can lead to local or remote code execution.

If the shell is invoked explicitly via ``shell=True``, it is the responsibility of
the application to ensure that the input is escaped properly.
The ``shlex.quote`` function can be used for this purpose:

.. code-block:: python

   import shlex
   subprocess.call(['ls', shlex.quote(input_arg)], shell=True)

See `Subprocess security considerations`_ for more information.

.. _`Subprocess functions`: https://docs.python.org/3/library/subprocess.html
.. _`Subprocess security considerations`: https://docs.python.org/3/library/subprocess.html#security-considerations
