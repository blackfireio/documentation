Organizations and Environments
==============================

.. include-twig:: `youtube-iframe`
    :title: Organizations and Environments
    :src: https://www.youtube-nocookie.com/embed/_lLyz7Xpay8?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

In this video, we explore how to organize your projects and subscriptions in Blackfire.

Whether you manage multiple clients or work across different stages of development,
understanding how to use Blackfire's organizational tools best is crucial.

Blackfire offers a flexible structure with organizations and environments
allowing you to set things up exactly how you need them for your specific workflow.

To start, let's break down what a :term:`Blackfire Organization <Organization>` is.

Organizations
~~~~~~~~~~~~~

An organization in Blackfire is directly linked to a subscription. You could
think of it as a container that groups your projects, users, and resources
together. Depending on your role, you might be the owner or a member of one or
several organizations, each with its own subscription.

This setup is handy for agencies, for example. Some agencies prefer to have one
organization and therefore one subscription per client. This way, they can easily
manage billing and permissions separately for each client. It keeps everything
clean and well defined with different teams working in dedicated eras without
any overlap.

Others prefer a different approach and like to have a single organization. They
add or remove extra users or environments as needed.

This allows them to centralize everything under one subscription, while giving
them the flexibility to scale up as projects grow.

Either approach can work. It all depends on what suits your workflow best.

Environments
~~~~~~~~~~~~

Now, let's talk about **environments**. A :doc:`Blackfire environment </reference-guide/environments>` is essentially a collaborative workspace, where you and your team can collect
observability data.

You can purchase as many environments as you need for your organization.
Environments can help you distinguish between different projects, as well as
different server types, such as production, staging, or development. Think of
each Blackfire environment as an observability silo for a specific part of your
work.

We typically recommend creating one environment per application and per server
type. For example, one for your production server, one for staging, and one for
development. This setup helps you ensure you get the most accurate relevant data
for each aspect of your application. However, the great thing about Blackfire is
that you are in control.

If you prefer to work with fewer environments, or even just a single one, with
everything in it, you absolutely can.

Keep in mind that while it might simplify your setup, it could also affect the
quality of your data, as it will mix metrics from different contexts.
