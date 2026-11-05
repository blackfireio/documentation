The $more_entropy option of uniqid() should be used
===================================================

The `uniqid()`_ function takes a second argument called ``$more_entropy``.

Without ``$more_entropy``, ``uniqid()`` only encodes the current time in
microseconds, so two processes calling it during the same microsecond get the
same value. With ``$more_entropy`` set to ``true``, PHP appends a random number
to the value.

Up to PHP 7.1, omitting ``$more_entropy`` also called ``usleep(1)``, pausing
your entire application, failed on Cygwin, and yielded non-unique values on
Windows. Since PHP 7.2, ``uniqid()`` waits for the next microsecond in both
cases, without sleeping.

Therefore, the only way to make ``uniqid()`` generate reasonably unique values
is to call it with ``true`` as second argument (``uniqid('...', true)``).

.. _`uniqid()`: https://www.php.net/manual/en/function.uniqid.php
