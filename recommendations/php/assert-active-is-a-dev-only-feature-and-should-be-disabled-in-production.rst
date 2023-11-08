"assert.active" is a dev-only feature and should be disabled in production
==========================================================================

The `assert.active`_ ini setting enables the execution of the assertions defined
with the `assert()`_ function. These asserts are used for debugging purposes,
usually to check the value of functions parameters.

As this setting can be deactivated in the PHP configuration file, it makes your
application non portable and therefore should be used only while developing
applications.

If you want to ensure business rules in your code, use `Exceptions`_ instead.

It's strongly recommended to disable this setting in production in your ``php.ini``
configuration using ``assert.active=off``. This will also bring you extra performance
from not running these assertions in production.

.. _`assert()`: https://www.php.net/manual/en/function.assert.php
.. _`Exceptions`: https://www.php.net/manual/en/language.exceptions.php
.. _`assert.active`: https://www.php.net/manual/en/info.configuration.php#ini.assert.active
