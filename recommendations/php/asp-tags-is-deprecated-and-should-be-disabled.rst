"asp_tags" is deprecated and should be disabled
===============================================

The `asp_tags`_ ini setting allowed developers to use an alternative
to the PHP open tag (``<% ... %>``) instead of the standard one (``<?php ... ?>``).

This settings is now deprecated and has been removed in PHP 7.

Moreover, as this setting can be disabled, using asp tags makes your code non
portable, therefore you should not use them.

It's recommended to disable this setting in your ``php.ini`` configuration using
``asp_tags=off``.

.. _`asp_tags`: https://www.php.net/manual/en/ini.core.php#ini.asp-tags
