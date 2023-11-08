The Mcrypt extension is deprecated and should not be used
=========================================================

The `mcrypt PHP extension`_ is an interface to the `mcrypt library`_, which
allows to encrypt/decrypt contents using a wide variety of algorithms such as
DES, Blowfish, AES/Rijndael, etc.

The mcrypt library development was abandoned in 2007. Therefore, `it was decided`_
to deprecate the ``mcrypt`` extension starting from PHP 7.1 version and remove it
completely in the next PHP version. Use instead the `OpenSSL PHP extension`_.

.. _`mcrypt PHP extension`: https://www.php.net/manual/en/book.mcrypt.php
.. _`mcrypt library`: https://sourceforge.net/projects/mcrypt/
.. _`it was decided`: https://wiki.php.net/rfc/mcrypt-viking-funeral
.. _`OpenSSL PHP extension`: https://www.php.net/manual/en/book.openssl.php
