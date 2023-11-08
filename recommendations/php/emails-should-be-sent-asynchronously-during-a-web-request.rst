Emails should be sent asynchronously during a Web request
=========================================================

Sending emails, even if they are simple and contain no attachments, is one of
the slowest tasks for web applications. They require to make network connections
to external services and wait for their response.

If your application sends emails in production, the response time will increase
and the users will perceive an overall slow down. Besides the performance impact,
there is also a scalability issue, because the PHP process can't serve any other
HTTP request while sending the emails.

Fortunately, most of the emails don't require to be sent immediately and users
can wait a few seconds or minutes to receive them. Therefore, the solution to
this problem is to not send emails synchronously and wait until the application
frees some resources.

The actual way of implementing this solution depends on the PHP application
being used.

In Symfony applications, this technique is called *"email spooling"* and it
requires you to define some configuration for the ``swiftmailer`` service:

.. code-block:: php

    # app/config/config.yml
    swiftmailer:
        # ...
        spool:
            # save the emails as files inside the given directory
            type: file
            path: /path/to/spooldir

Then, use the ``swiftmailer:spool:send`` command to flush the queue of pending
emails. Read the `How to Spool Emails`_ tutorial in the Symfony documentation to
learn more about this command.

In Laravel applications this technique is called *"queueing mail"*. First you
must configure a queue and then use the ``queue()`` method of the ``Mail`` façade:

.. code-block:: php

    Mail::queue('emails.welcome', $data, function ($message) {
        // ...
    });

Read the `Mail chapter`_ in the Laravel documentation to learn how to delay
email messages in the queues and how to push them to specific queues.

.. _`Mail chapter`: https://laravel.com/docs/5.1/mail#queueing-mail
.. _`How to Spool Emails`: https://symfony.com/doc/current/cookbook/email/spool.html
