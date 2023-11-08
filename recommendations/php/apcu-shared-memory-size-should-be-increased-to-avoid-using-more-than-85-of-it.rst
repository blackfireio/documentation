APCu shared memory size should be increased to avoid using more than 85% of it
==============================================================================

`APCu`_ (APC User Cache), provides a simple API to cache and retrieve data in
PHP applications. This data is stored in shared memory segments that can be
configured using these settings:

* `apc.shm_size`_ configures the size of each shared memory segment. It supports
  the ``K``, ``M`` and ``G`` suffixes (e.g. ``128K``, ``4M``, etc.)
* `apc.shm_segments`_ configures the total number of segments created for APCu.

It's recommended to increase the APC shared memory size gradually as much as
needed to avoid using more than 85% of its total size.

.. _`APCu`: https://www.php.net/manual/en/book.apcu.php
.. _`apc.shm_size`: https://www.php.net/manual/en/apc.configuration.php#ini.apc.shm-size
.. _`apc.shm_segments`: https://www.php.net/manual/en/apc.configuration.php#ini.apc.shm-segments
