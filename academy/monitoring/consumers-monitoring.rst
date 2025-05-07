Consumers Monitoring
====================

.. include-twig:: `youtube-iframe`
    :title: Consumesd Monitoring
    :src: https://www.youtube-nocookie.com/embed/48uEe1dINNA?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

Today, we are going to learn how to :doc:`enable Blackfire monitoring for CLI
commands and consumers </monitoring-cookbooks/consumers-monitoring>`. Whether
you're running custom scripts, background workers, or managing queue consumers,
Blackfire helps you gain performance insights right where you need them.

Let's dive in!

To view monitoring data for CLI commands or consumers, simply toggle the web CLI
dropdown in the Blackfire Monitoring Interface. This switch lets you focus on
either your web traffic or CLI processes, making it easy to access the right
data at the right time.

Now let's set up **CLI monitoring**. Unlike for the HTTP traffic, CLI commands
and consumers require manual instrumentation. It's up to you to decide if you
want to monitor long running processes or individual granular jobs.

Here's how it works for PHP applications. Use the ``\BlackfireProbe::startTransaction``
method to start the instrumentation. Pass a descriptive name for your CLI command,
like "My CLI command", so it's easy for you to identify it later. After running
your code, stop the transaction with the ``\BlackfireProbe::stopTransaction()`` method.

As for Python, start the transaction with the ``apm.start_transaction()`` method.
Use ``apm.set_transaction_name()`` to assign a descriptive name. Once the script
is complete, stop the transaction with ``apm.stop_transaction()``.

The key is manually controlling and naming the transaction so Blackfire knows
precisely what to monitor.

Blackfire also offers integration with popular tools and frameworks to make
things easier, such as :doc:`Symfony Messenger </php/integrations/symfony/messenger>`,
:doc:`Symfony CLI commands </php/integrations/symfony/cli-commands-monitoring>`,
:doc:`Laravel Artisan </php/integrations/laravel/artisan>`,
:doc:`Horizon and queue services </php/integrations/laravel/horizon>`.
Behind the scene, those integrations use the same logic we have seen.

And that's it! You've learned how to enable CLI monitoring for both PHP and
Python applications, name transactions effectively, and leverage native
integration for added convenience.

Start applying these techniques to monitor your CLI workflows today, and as
always, stay in control with Blackfire.
