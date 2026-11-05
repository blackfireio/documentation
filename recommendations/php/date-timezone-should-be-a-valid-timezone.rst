"date.timezone" should be a valid timezone
==========================================

The `date.timezone`_ ini setting sets the default timezone for PHP date and time functions.

Since PHP 7.0, an empty value falls back to ``UTC`` without any warning, and
``UTC`` is the default value since PHP 8.2, so Blackfire accepts an empty
value. An invalid value triggers a warning and PHP uses ``UTC`` instead, which
may not be the timezone your application expects.

The current timezone does not seem to be a valid one, please
refer to the `documentation`_ to get the list of available timezones.

.. _`date.timezone`: https://www.php.net/manual/en/datetime.configuration.php#ini.date.timezone
.. _`documentation`: https://www.php.net/manual/en/timezones.php
