Symfony Routing route collection should not be called during a Web request
==========================================================================

In Symfony applications, the method ``Symfony\Component\Routing\RouterInterface::getRouteCollection`` is very slow
as it recomputes all routes from their definitions.

It should only be used during the cache warmup.

If you are looking for a way to know if a route is defined or not, you can use the following code:

.. code-block:: php

    use Symfony\Component\Routing\Exception\RouteNotFoundException;

    $found = true;
    try {
        // Instance of Symfony\Component\Routing\RouterInterface / Symfony\Component\Routing\Generator\UrlGenerator
        $router->generate('MY_ROUTE');
    } catch (RouteNotFoundException $e) {
        $found = false;
    }

.. _`Router interface`: https://api.symfony.com/4.0/Symfony/Component/Routing/RouterInterface.html
