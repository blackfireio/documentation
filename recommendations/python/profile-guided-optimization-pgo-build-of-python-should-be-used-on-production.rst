Profile Guided Optimization (PGO) build of Python should be used on production
==============================================================================

When Python is compiled via PGO (Profile Guided Optimization), it usually runs roughly
``10%``-``20%`` faster.

Most Linux/Windows distributions come with PGO enabled binaries. However,
there might be some exceptions, e.g.: Ubuntu as of 2021. For macOS, you might 
need to compile it yourself. See https://bugs.python.org/issue41181 for details.

You can check if the Python interpreter is compiled with PGO by running the following command:

.. code-block:: python

   python -c "import sysconfig; print('-fprofile-use' in (sysconfig.get_config_var('PY_CFLAGS') + sysconfig.get_config_var('PY_CFLAGS_NODIST')))"

You can get more details on the subject:

- https://www.activestate.com/blog/python-performance-boost-using-profile-guided-optimization/
- https://bugs.python.org/issue41181
