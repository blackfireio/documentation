"max_execution_time" should be greater or equal to 0 seconds on the CLI
=======================================================================

The `max_execution_time`_ ini setting defines the maximum time in seconds a
script is allowed to run before it is automatically terminated.

Using a negative value for this settings is invalid. In order to disable
this, use the ``0`` value.

It's strongly recommended to update this setting in your ``php.ini``
configuration using ``max_execution_time=0``.

.. _`max_execution_time`: https://www.php.net/manual/en/info.configuration.php#ini.max-execution-time
