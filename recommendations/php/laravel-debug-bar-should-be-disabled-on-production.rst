Laravel debug bar should be disabled on production
==================================================

`Laravel Debugbar`_ is a package that integrates `PHP Debug Bar`_ with Laravel.
It provides various information thanks to various collectors (SQL queries, routes,
views, events...).

The Laravel Debugbar is meant for development only and **should never be enabled in
production, as it can slow the application down (because it has to gather data)**.

.. _`Laravel Debugbar`: https://github.com/barryvdh/laravel-debugbar

.. _`PHP Debug Bar`: http://phpdebugbar.com/
