Symfony config resource tracking should be disabled in production
=================================================================

Symfony applications use the `Config component`_ to process, combine and
validate all their configuration files. The final processed configuration
doesn't have to be regenerated for each request, because configuration files
rarely change, even while developing the application.

The configuration cache stores the last modification time of the original files
to check if they must be processed again because they changed since the last
request. This checking process requires to make calls to the ``filemtime()``
function on lots of different files. This is a time-consuming task and that's
why you should not use Symfony config checks in production.

In practice, avoid calling to the ``isFresh()`` method on classes like
``ConfigCache`` and ``ResourceCheckerConfigCache`` during the application
execution. Moreover, make sure that all the configuration is fully processed
before running the application in the production environment.

If your application doesn't make any configuration checks, you might see this
recommendation because of some third-party bundle enabled in the application.

.. _`Config component`: https://symfony.com/components/Config
