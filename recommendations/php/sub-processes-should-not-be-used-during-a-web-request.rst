Sub-processes should not be used during a Web request
=====================================================

In web applications it's common to perform some tasks during requests and before
sending back the response to the users. For example, when a new user signs up
you may want to resize the avatar image and distribute it across your CDN servers.

Creating sub-processes to perform those tasks is simple thanks to the
`Symfony Process component`_. However, executing tasks during web requests will
make them slower and the user will perceive a worse performance. That's why you
should not run sub-processes in production.

The solution is to use a `message broker`_, often called a *queue system*, to
schedule the tasks for later execution. Therefore, the user gets an immediate
response and the tasks get executed asynchronously when the server has enough
free resources.

.. _`Symfony Process component`: https://symfony.com/components/Process
.. _`message broker`: https://en.wikipedia.org/wiki/Message_broker
