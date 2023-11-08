Only one AMQP connection should be used
=======================================

`AMQP`_  is an open standard application layer protocol for message-oriented
middleware, such as the `RabbitMQ`_ message broker. Before sending and receiving
messages from AMQP brokers, applications must instantiate a client to connect to
those message brokers.

Simple applications host different services (RabbitMQ, databases, web server,
etc.) on the same machine, but most of the times RabbitMQ is hosted on a
different server. Therefore, connecting to AMQP brokers introduces some overhead
due to the TCP/IP connection.

Blackfire detects the connections established with the popular `PHP AMQP`_ and
`PECL ampq`_ libraries. Unless configured differently, you'll see this
recommendation when establishing more than one AMQP connection during the
application execution.

.. _`AMQP`: https://en.wikipedia.org/wiki/Advanced_Message_Queuing_Protocol
.. _`RabbitMQ`: https://en.wikipedia.org/wiki/RabbitMQ
.. _`PHP AMQP`: https://github.com/php-amqplib/php-amqplib
.. _`PECL ampq`: https://pecl.php.net/package/amqp
