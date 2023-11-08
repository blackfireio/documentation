"date.timezone" should be a valid timezone
==========================================

The `date.timezone`_ ini setting sets the default timezone for PHP date and time functions.

Since PHP 5.1, the engine uses this information to compare dates.
If this setting is not defined, prior to PHP 5.4.0, it reads the ``TZ``
environment variable if not empty, or triggers a warning.

Even though PHP 7 has a safe default, we recommend setting this value. It will make your configuration more robust.

This is why the timezone should be defined so PHP can compare dates accurately.

The current timezone does not seem to be a valid one, please
refer to the `documentation`_ to get the list of available timezones.

.. _`date.timezone`: https://www.php.net/manual/en/datetime.configuration.php#ini.date.timezone
.. _`documentation`: https://www.php.net/manual/en/timezones.php
