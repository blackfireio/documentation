Logs should not be sent to the browser in production
====================================================

`FirePHP`_, `ChromePhp`_ and `PHP Console`_ are some of the most popular tools
that allow PHP applications to send log messages to the Mozilla Firefox and
Google Chrome browsers. Some PHP frameworks and logging libraries, such as
`Monolog`_, provide seamless integration with those utilities.

Viewing log messages right inside the browser may be convenient while developing
the application, but it shouldn't be enabled in the production servers. In
addition to potentially disclosing sensitive information, sending log messages
to the browser hurts the overall application performance.

.. _`FirePHP`: https://addons.mozilla.org/es/firefox/addon/firephp/
.. _`ChromePhp`: https://github.com/ccampbell/chromephp
.. _`PHP Console`: https://github.com/barbushin/php-console
.. _`Monolog`: https://github.com/Seldaek/monolog
