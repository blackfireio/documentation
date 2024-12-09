Deprecated functions should not be used
=======================================

The PHP language evolves, and some of its functions are deprecated in the current
version, before getting removed in the next one. If you use a deprecated function,
you should be aware that it will make PHP upgrades more difficult.

Blackfire keeps an up-to-date list of deprecated functions.

**Deprecated in PHP 5.3**

https://www.php.net/manual/en/migration53.deprecated.php

* ``call_user_method()``

This function was deprecated in PHP 4.1.0 and removed in PHP 7.0.0. Use ``call_user_func()`` instead.

* ``call_user_method_array()``

This function was deprecated in PHP 4.1.0 and removed in PHP 7.0.0. Use ``call_user_func_array()`` instead.

* ``define_syslog_variables()``

This function was deprecated in PHP 5.3.0 and removed in PHP 5.4.0.

* ``dl()``

This function was removed from most SAPIs in PHP 5.3.0, and was removed from PHP-FPM in PHP 7.0.0.

* ``ereg()``

This function was deprecated in PHP 5.3.0 and removed in PHP 7.0.0. Use ``preg_match()`` instead.

* ``ereg_replace()``

This function was deprecated in PHP 5.3.0 and removed in PHP 7.0.0. Use ``preg_replace()`` instead.

* ``eregi()``

This function was deprecated in PHP 5.3.0 and removed in PHP 7.0.0. Use ``preg_match()`` with the *i* modifier instead.

* ``eregi_replace()``

This function was deprecated in PHP 5.3.0 and removed in PHP 7.0.0. Use ``preg_replace()`` with the *i* modifier instead.

* ``magic_quotes_runtime()``

This function was deprecated in PHP 5.3.0 and removed in PHP 7.0.0.

* ``mcrypt_generic_end()``

This function was deprecated in PHP 5.3.0 and removed in PHP 7.0.0. Use ``mcrypt_generic_deinit()`` instead.

* ``mysql_db_query()``

This function was deprecated in PHP 5.3.0 and removed in PHP 7.0.0. Use PDO instead.

* ``mysql_escape_string()``

This function was deprecated in PHP 4.3.0 and removed in PHP 7.0.0. Use PDO instead.

* ``mysql_list_tables()``

This function was deprecated in PHP 4.3.0 and removed in PHP 7.0.0. Use PDO instead.

* ``session_is_registered()``

This function was deprecated in PHP 5.3.0 and removed in PHP 5.4.0.

* ``session_register()``

This function was deprecated in PHP 5.3.0 and removed in PHP 5.4.0.

* ``session_unregister()``

This function was deprecated in PHP 5.3.0 and removed in PHP 5.4.0.

* ``set_magic_quotes_runtime()``

This function was deprecated in PHP 5.3.0 and removed in PHP 7.0.0.

* ``set_socket_blocking()``

This function was deprecated in PHP 5.3.0 and removed in PHP 7.0.0. Use ``stream_set_blocking()`` instead.

* ``split()``

This function was deprecated in PHP 5.3.0 and removed in PHP 7.0.0. Use ``explode()``, ``str_split()`` or
``preg_split()`` instead.

* ``spliti()``

This function was deprecated in PHP 5.3.0 and removed in PHP 7.0.0. Use ``preg_split()`` with the *i* modifier instead.

* ``sql_regcase()``

This function was deprecated in PHP 5.3.0 and removed in PHP 7.0.0. Use ``preg_match()`` and ``preg_quote()`` instead.


**Deprecated in PHP 5.4**

https://www.php.net/manual/en/migration54.deprecated.php

* ``mysql_list_dbs()``

This function was deprecated in PHP 5.4.0 and removed in PHP 7.0.0. Use PDO instead.


**Deprecated in PHP 5.5**

https://www.php.net/manual/en/migration55.deprecated.php

* ``datefmt_set_timezone_id()``
* ``mcrypt_cbc()``, ``mcrypt_cfb()``, ``mcrypt_ecb()``, ``mcrypt_ofb()``

You can replace ``mcrypt_cbc()``, ``mcrypt_cfb()``, ``mcrypt_ecb()`` and ``mcrypt_ofb()`` by ``mcrypt_generic()``
and ``mdecrypt_generic()``.
Please note that the mcrypt extension has fully been deprecated in PHP 7.1


**Deprecated in PHP 7.0**

https://www.php.net/manual/en/migration70.deprecated.php

* ``ldap_sort()``


**Deprecated in PHP 7.2**

https://www.php.net/manual/en/migration72.deprecated.php

* ``__autoload()``

The ``__autoload`` is now deprecated in favor of ``spl_autoload_register`` as it is much more flexible allowing chained
autoloaders to be registered and as these two autoload registration methods are incompatible.

.. code-block:: php

    function __autoload($className) {
        include $className.'.php';
    }

    // Should be replaced by

    spl_autoload_register(function($className) {
        include $className.'.php';
    });


* ``create_function()``

``create_function`` was a technique used before PHP 5.3 and based on `eval` to create lambda functions. Due to its nature,
this function is not performant and is not needed anymore. It should not be used anymore.

.. code-block:: php

    create_function('$a, $b', 'return strlen($b) - strlen($a);');

    // Should be replaced by

    function($a, $b) {
        return strlen($b) - strlen($a);
    });


* ``gmp_random()``

``gmp_random`` generates a random number between ``0`` and ``2**($n*BITS_PER_LIMB)-1``, where ``BITS_PER_LIMB`` is platform
specific and not accessible for userland code. Therefore, this function is tied to the platform and should not be used.

PHP 5.6 introduced ``gmp_random_bits()`` and ``gmp_random_range()`` functions to solve this issue. These functions should
always be preferred over ``gmp_random()``.

.. code-block:: php

    gmp_random();

    // Should be replaced by

    gmp_random_range($min, $max); // or
    gmp_random_bits($bites);


* ``each()``

``each`` is a technique that can be used to iterate over an array, similarly to `foreach`. However, it is inferior to
foreach in every way, being 10 times slower and posing problems to the engine. Therefore, `foreach` should always be
preferred.

.. code-block:: php

    while (list($key, $val) = each($array)) {
        echo $key.' => '.$val.'<br />';
    }

    // Should be replaced by

    foreach ($array as $key => $value) {
        echo $key.' => '.$val.'<br />';
    }


**Deprecated in PHP 7.3**

https://www.php.net/manual/en/migration73.deprecated.php

* ``mbereg_*``

``mbereg_*()`` aliases have been deprecated. Use the corresponding ``mb_ereg_*()`` variants instead.

* ``image2wbmp``

``image2wbmp()`` has been deprecated.

* Striptags Streaming

The ``fgetss`` function and variants (``SplFileObject::fgetss`` and ``gzgetss``) have been deprecated.

**Deprecated in PHP 7.4**

https://www.php.net/manual/en/migration74.deprecated.php

* ``ReflectionType::__toString``

``ReflectionType::__toString()`` has been deprecated in favor of ReflectionNamedType::getName()

* ``ldap_control_paged_result_response`` and ``ldap_control_paged_result``

``ldap_control_paged_result_response()`` and ``ldap_control_paged_result()`` are deprecated.
Pagination controls can be sent along with ``ldap_search()`` instead.

* ``restore_include_path``

``restore_include_path()`` function is deprecated. It can be replaced by ``ini_restore('include_path')``.

* ``ezmlm_hash``

The ``ezmlm_hash`` function is deprecated.

* ``money_format``

The ``money_format`` function is deprecated. It can be replaced by the intl ``NumberFormatter`` functionality.

* ``convert_cyr_string``

The ``convert_cyr_string()`` function is deprecated. It can be replaced by one of ``mb_convert_string()``, ``iconv()`` or ``UConverter``.

* ``hebrevc``

The ``hebrevc()`` function is deprecated. It can be replaced with ``nl2br(hebrev($str))`` or, preferably, the use of Unicode RTL support.

* ``get_magic_quotes_gpc`` and ``get_magic_quotes_runtime``

``get_magic_quotes_gpc()`` and ``get_magic_quotes_runtime()`` functions are deprecated. They always return ``FALSE``.

* ``is_real``

The ``is_real()`` function is also deprecated, use ``is_float()`` instead.

**Deprecated in PHP 8.0**

Please find the documentation about deprecations in `the official PHP 8.0 migration guide`_.

**Deprecated in PHP 8.1**

Please find the documentation about deprecations in `the official PHP 8.1 migration guide`_.

**Deprecated in PHP 8.2**

* ``utf8_decode`` and ``utf8_encode``

The ``utf8_decode()`` and ``utf8_encode()`` functions are deprecated. Although their names were not explicit,
they actually only converted UTF-8 strings to ISO-8859-1 and vice versa. They can be replaced by ``mb_convert_encoding()``.

.. code-block:: php

    utf8_decode($string);
    utf8_encode($otherString);

    // Should be replaced by

    mb_convert_encoding($string, 'UTF-8', 'ISO-8859-1');
    mb_convert_encoding($otherString, 'ISO-8859-1', 'UTF-8');

Please find the documentation about deprecations in `the official PHP 8.2 migration guide`_.

**Deprecated in PHP 8.3**

Please find the documentation about deprecations in `the official PHP 8.3 migration guide`_.

**Deprecated in PHP 8.4**

Please find the documentation about deprecations in `the official PHP 8.4 migration guide`_.

.. _`the official PHP 8.0 migration guide`: https://www.php.net/manual/en/migration80.deprecated.php
.. _`the official PHP 8.1 migration guide`: https://www.php.net/manual/en/migration81.deprecated.php
.. _`the official PHP 8.2 migration guide`: https://www.php.net/manual/en/migration82.deprecated.php
.. _`the official PHP 8.3 migration guide`: https://www.php.net/manual/en/migration83.deprecated.php
.. _`the official PHP 8.4 migration guide`: https://www.php.net/manual/en/migration84.deprecated.php
