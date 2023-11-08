Operations during fastcgi_finish_request should be light
========================================================

`fastcgi_finish_request`_ is a built-in PHP function available in a PHP-FPM
context.

Its role is to flush all the HTTP response data to the client and to allow the
application to "finish" the request, e.g. performing time-consuming operations,
while leaving the connection to the client open.

It is possible to call this function directly, or via the framework your
application is using:

- `kernel.terminate Symfony event`_
- `Laravel Terminable middleware`_

Pitfalls
--------

While it can be helpful to trigger operations once the response has been sent
to the client (e.g. to send e-mails or to emulate asynchronous tasks), the
technique is not exempt of pitfalls:

- Errors are hidden;
- The PHP worker is still occupied, which can lead to a `dog-piling effect`_
  in your FPM threads;
- Sessions may remain locked;
- Filesystem or database locks may not be released, forcing other clients to wait
  for the current PHP worker to finish.

Using Asynchronous Processes
----------------------------

One of the solutions is to use asynchronous processes,
with the help of message brokers such as RabbitMQ, Redis, or Amazon SQS.

Setting-up message consumers can be eased by the framework your application is
using, e.g.:

- `Symfony Messenger component`_
- `Laravel Queues`_

.. _`fastcgi_finish_request`: https://www.php.net/fastcgi_finish_request
.. _`kernel.terminate Symfony event`: https://symfony.com/doc/current/components/http_kernel.html#component-http-kernel-kernel-terminate
.. _`Laravel Terminable middleware`: https://laravel.com/docs/8.x/middleware#terminable-middleware
.. _`dog-piling effect`: https://en.wikipedia.org/wiki/Cache_stampede
.. _`Symfony Messenger component`: https://symfony.com/doc/current/components/messenger.html
.. _`Laravel Queues`: https://laravel.com/docs/8.x/queues#introduction
