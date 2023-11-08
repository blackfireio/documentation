"memory_limit" should be greater than "post_max_size"
=====================================================

The `post_max_size`_ ini setting sets the maximum size of post data allowed in
an HTTP request. This setting also affects file upload. `memory_limit`_ should
be larger than `post_max_size`.

Note that if the size of post data is greater than `post_max_size`, the `$_POST`
and `$_FILES` superglobals are empty.

.. _`post_max_size`: https://www.php.net/manual/en/ini.core.php#ini.post-max-size
.. _`upload_max_filesize`: https://www.php.net/manual/en/ini.core.php#ini.upload-max-filesize
.. _`memory_limit`: https://www.php.net/manual/en/ini.core.php#ini.memory-limit
