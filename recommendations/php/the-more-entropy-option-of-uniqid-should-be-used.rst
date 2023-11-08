The $more_entropy option of uniqid() should be used
===================================================

The `uniqid()`_ function takes a second argument called ``$more_entropy``.

If ``$more_entropy`` is omitted or set to ``false``:

* on Cygwin, the function does not work;
* on Windows, it yields non-unique values;
* on other OSes, it calls ``usleep(1)``, pausing your entire application for 1 microsecond.

Therefore, the only way to make ``uniqid()`` generate reasonably unique values
is to call it with ``true`` as second argument (``uniqid('...', true)``).

.. _`uniqid()`: https://www.php.net/manual/en/function.uniqid.php
