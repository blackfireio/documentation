Laravel [language: PHP]
=======================

By default, **Blackfire works seamlessly with any application built with Laravel**,
like any PHP application.

:doc:`Install Blackfire for PHP </install/php>`.

.. _laravel-transaction-names:

Transaction names
-----------------

The **Probe** names your HTTP transactions after the code that handles them:

* A controller action takes the controller class and method, like
  ``App\Http\Controllers\UserController::show``.
* A closure route takes its route name when it has one, like ``users.show``,
  and its method and URI otherwise, like ``GET /users/{id}``. ``HEAD``
  requests share the name of the matching ``GET`` route.
* A page route declared with ``Route::view``, ``Route::redirect``,
  ``Route::livewire`` or ``Route::inertia`` follows the same rule as a closure
  route, like ``dashboard`` or ``GET /settings``, instead of sharing the name of
  the framework controller that serves all of them.
* A Livewire 3 or 4 update takes the component name and the first method it
  calls, like ``livewire counter@increment``, so each interaction gets its own
  transaction. An update that calls no method, such as a property change, takes
  the component name alone, like ``livewire counter``.

When a route dispatches another route, the outer route names the transaction.

Naming closure routes, page routes and Livewire updates requires Blackfire PHP Probe
``>= 2026.11.0``.

However, in some cases, you may want to go further and :doc:`monitor your
queue workers </php/integrations/laravel/horizon>`, automatically with the
**Probe** or with the SDK, or :doc:`monitor Artisan commands
</php/integrations/laravel/artisan>`.

For these advanced cases, Blackfire provides the following integrations with
Laravel:

.. toctree::
    :maxdepth: 1

    artisan
    horizon
    octane

The Laravel ecosystem also offers extensive support for Blackfire. Find more about:

* Blackfire on `Laravel Homestead <https://laravel.com/docs/master/homestead#profiling-applications-with-blackfire>`_

* Blackfire on `Laravel Vapor <https://flareapp.io/blog/8-installing-blackfire-on-laravel-vapor#1-installing-the-blackfire-agent>`_
