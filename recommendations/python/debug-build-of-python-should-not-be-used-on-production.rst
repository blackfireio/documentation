Debug build of Python should not be used on production
======================================================

A Debug build of Python adds various hooks to the memory allocator, reference 
counting functions, and disables compiler optimizations. Due to these, it might 
be substantially slower. On production, using an optimized release version of 
Python is always recommended.

You can check if the Python interpreter is compiled in Debug mode via the following:

.. code-block:: python

   python -c "import sysconfig; print(bool(sysconfig.get_config_var('Py_DEBUG')))"
