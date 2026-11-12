Symfony Messenger messages should not be retried during a Web request
=====================================================================

Since Symfony 8.2, the ``sync://`` transport retries a failing message when
its DSN sets ``retry=true``. Retries run immediately, inside the Web request,
so each one adds the cost of the handler to the response time.

When the last retry fails and the DSN sets ``failure_transport=true``,
Messenger sends the message to the failure transport instead of throwing an
exception. The page returns a successful response, but the work of the message
never happened.

Route the message to an asynchronous transport instead. A worker then handles
it, retries it with a delay when it fails, and the user gets the response
without waiting:

.. code-block:: php

    use Symfony\Component\Messenger\Attribute\AsMessage;

    #[AsMessage('async')]
    final class PaymentReceived
    {
    }

When the message must be handled during the request, fix the failure of its
handler, and check the messages left in the failure transport with
``messenger:failed:show``.
