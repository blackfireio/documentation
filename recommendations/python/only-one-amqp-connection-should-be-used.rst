Only One AMQP Connection Should Be Used
=======================================

`AMQP`_  is an open standard application layer protocol for message-oriented
middleware, such as the `RabbitMQ`_ message broker. Before sending and receiving
messages from AMQP brokers, applications must instantiate a client to connect to
those message brokers.

Simple applications host different services (RabbitMQ, databases, web server,
etc.) on the same machine, but most of the times RabbitMQ is hosted on a
different server. Therefore, connecting to AMQP brokers introduces some overhead
due to the TCP/IP connection.

Blackfire detects the connections established with the popular `pyamqp`_,
`librabbitmq`_ and `pika`_ libraries. Unless configured differently, you'll see
this recommendation when establishing more than one AMQP connection during the
application execution.

.. _`AMQP`: https://en.wikipedia.org/wiki/Advanced_Message_Queuing_Protocol
.. _`RabbitMQ`: https://en.wikipedia.org/wiki/RabbitMQ
.. _`pyamqp`: https://github.com/celery/py-amqp
.. _`librabbitmq`: https://github.com/celery/librabbitmq
.. _`pika`: https://github.com/pika/pika
