"post_max_size" should be greater than "upload_max_filesize"
============================================================

The `upload_max_filesize`_ ini setting sets the maximum size of an uploaded
file. To upload large files, the `post_max_size`_ value must be larger than
`upload_max_filesize`_.

.. _`upload_max_filesize`: https://www.php.net/manual/en/ini.core.php#ini.upload_max_filesize
.. _`post_max_size`: https://www.php.net/manual/en/ini.core.php#ini.post-max-size
