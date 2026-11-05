"assert.active" is a dev-only feature and should be disabled in production
==========================================================================

The `assert.active`_ ini setting enables the checks of the assertions defined
with the `assert()`_ function. These asserts are used for debugging purposes,
usually to check the value of functions parameters.

As this setting can be deactivated in the PHP configuration file, it makes your
application non portable and therefore should be used only while developing
applications.

If you want to ensure business rules in your code, use `Exceptions`_ instead.

It's recommended to disable this setting in production in your ``php.ini``
configuration using ``assert.active=off``. PHP still evaluates the asserted
expressions with this setting disabled, so use ``zend.assertions=-1`` to skip
them and get the performance gain, as explained in
:doc:`/recommendations/php/zend-assertions-is-a-dev-only-feature-and-should-be-disabled-in-production`.

Blackfire only checks this setting up to PHP 8.2, as disabling it is deprecated
since PHP 8.3.

.. _`assert()`: https://www.php.net/manual/en/function.assert.php
.. _`Exceptions`: https://www.php.net/manual/en/language.exceptions.php
.. _`assert.active`: https://www.php.net/manual/en/info.configuration.php#ini.assert.active
