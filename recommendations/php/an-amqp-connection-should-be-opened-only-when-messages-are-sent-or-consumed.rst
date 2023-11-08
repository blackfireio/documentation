An AMQP connection should be opened only when messages are sent or consumed
===========================================================================

The `AMQP Specification`_ describes in the connections section that each
AMQP connection begins with an exchange of capabilities and limitations: after
establishing or accepting a TCP connection and sending the protocol header, each
peer sends an open frame before sending any other frames. The open frame
describes the capabilities and limits of that peer.

Therefore, establishing an AMPQ connection introduces a significant overhead due
to the TCP/IP connection and the initial frame exchange. If your application
does not send or consume messages, you should not connect to AMQP.

.. _`AMQP Specification`: https://docs.oasis-open.org/amqp/core/v1.0/amqp-core-complete-v1.0.pdf
