You should be in production mode in Magento 2
=============================================

Magento 2 can run using 3 different modes: ``default``, ``developer``, or ``production``.

The ``default`` mode is how Magento operates if no other mode is specified.
You should not use it.

You should run Magento in ``developer`` mode when you are extending or customizing it.

But when Magento is deployed to a production server, you should use the ``production`` mode.

If you want to learn more about it, `read the documentation`_.

How to switch to production mode
--------------------------------

1. First, check that you can run Magento CLI commands.
2. In the Magento root folder, run ``bin/magento deploy:mode:set production``.

This sets the mode to ``production``. Be careful, by default it will run the compilation processes.
The website will be in maintenance mode during this operation.

More details about the ``deploy:mode:set`` command in `the official documentation`_.

.. _`read the documentation`: https://devdocs.magento.com/guides/v2.2/config-guide/bootstrap/magento-modes.html
.. _`the official documentation`: https://devdocs.magento.com/guides/v2.2/config-guide/cli/config-cli-subcommands-mode.html
