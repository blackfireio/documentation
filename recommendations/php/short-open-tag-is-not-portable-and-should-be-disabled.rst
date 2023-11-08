"short_open_tag" is not portable and should be disabled
=======================================================

The `short_open_tag`_ ini setting allows developers to use the short alternative
of PHP open tag (``<? ... ?>``) instead of the standard one (``<?php ... ?>``).

As this setting can be disabled, using short open tags makes your code non
portable, therefore you should not use them.

It's recommended to disable this setting in your ``php.ini`` configuration using
``short_open_tag=off``.

Starting from PHP 5.4, this directive doesn't affect to the other short PHP tag
called "short echo" (``<?= ... ?>`` instead of ``<?php echo '...' ?>`` ), which
is `always enabled`_.

.. _`short_open_tag`: https://www.php.net/manual/en/ini.core.php#ini.short-open-tag
.. _`always enabled`: https://www.php.net/manual/en/ini.core.php#ini.short-open-tag
