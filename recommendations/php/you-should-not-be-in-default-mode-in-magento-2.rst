You should not be in default mode in Magento 2
==============================================

Magento 2 can run using 3 different modes: ``default``, ``developer``, or ``production``.

The ``default`` mode is how Magento operates if no other mode is specified.
You should not use it.

You should run Magento in ``developer`` mode when you are extending or customizing it.

But when Magento is deployed to a production server, you should use the ``production`` mode.

If you want to learn more about it, `read the documentation`_.

How to switch to developer or production mode
---------------------------------------------

1. First, check that you can run Magento CLI commands.
2. You have to choose between ``developer`` or ``production`` mode according to your needs.
3. In the Magento root folder you can run ``bin/magento deploy:mode:set MODE`` after changing ``MODE`` with the mode you want.

Be careful, the ``production`` mode will run the compilation processes and put the website in maintenance mode.

More details about the ``deploy:mode:set`` command in `the official documentation`_.

.. _`read the documentation`: https://devdocs.magento.com/guides/v2.2/config-guide/bootstrap/magento-modes.html
.. _`the official documentation`: https://devdocs.magento.com/guides/v2.2/config-guide/cli/config-cli-subcommands-mode.html
