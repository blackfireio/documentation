"detect_unicode" should be disabled as BOMs are not portable
============================================================

The `detect_unicode`_ ini setting, when enabled, checks scripts for `BOM (Byte Order Mark)`_
and see if the file contains valid multibyte characters.

This feature is known to produce issues when running `phar`_ executables and
should be disabled using ``detect_unicode=Off``.

You should also configure your code editor to never use BOMs.

.. _`detect_unicode`: https://www.php.net/manual/en/ini.core.php#ini.zend.detect-unicode
.. _`BOM (Byte Order Mark)`: https://en.wikipedia.org/wiki/Byte_order_mark
.. _`phar`: https://www.php.net/manual/en/book.phar.php
