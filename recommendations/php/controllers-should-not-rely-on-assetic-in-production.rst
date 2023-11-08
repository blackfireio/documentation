Controllers should not rely on Assetic in production
====================================================

`Assetic`_ is a PHP library to manage common tasks for web assets, such as
compiling, minifying and combining CSS and JavaScript files.

Assetic provides some special controllers that look for web assets modifications
and recompile them if needed. These controllers are very useful while developing
the application to increase your productivity. However, they consume a lot of
resources. For that reason, Blackfire detects any call performed to the Assetic
controllers in the production environment.

The easiest way to solve this problem is to leverage the caching mechanism of
Assetic. In production, compile, minify and combine all the web assets once and
dump the result into a cached file. If the application uses Symfony, you need to
execute this command:

.. code-block:: bash

    $ ./bin/console assetic:dump --env=prod --no-debug

An alternative solution is to replace Assetic by a non-PHP specific tool to
manage web assets, such as `webpack`_.

.. _`Assetic`: https://github.com/kriswallsmith/assetic
.. _`webpack`: https://webpack.github.io
