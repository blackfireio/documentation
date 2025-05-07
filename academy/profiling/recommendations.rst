Recommendations
===============

.. include-twig:: `youtube-iframe`
    :title: Triggering deterministic profiles
    :src: https://www.youtube-nocookie.com/embed/u7_-oDsWH_A?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

In this video, we are exploring :doc:`Blackfire's recommendation </testing-cookbooks/recommendations>`
system, which is your personal performance advisor based on your deterministic
profile data. Let's explore how this automated insight can help you build faster,
more secure applications.

Think of recommendations as your automated performance consultant. Every time
you profile your application, Blackfire analyzes your code and highlights
potential improvements based on industry best practices.

The beauty of recommendations is that they are context aware. For instance, what
you see will depend on whether you are in development or production, which
framework you are using, like :doc:`Symfony </php/integrations/symfony/index>`,
:doc:`Laravel </php/integrations/laravel/index>`, or :doc:`Django </python/integrations/django>`,
and your subscription level.

Blackfire's recommendations fall into three main categories:

- **Performance recommendations** help you optimize your code speed.
- **Quality recommendations**  are designed to help you adopt a better code structure.
- **Security recommendations** are here to protect your applications.

Let's look at a real example with this profile I just made.

 Notice how Blackfire not only identifies issues, but also explains why they
matter and how to fix them.

Here is where it gets really powerful. Any recommendation can be converted into
a test. You have the possibility to override a specific recommendation and
integrate it into your performance test by copying the YAML code provided and
then pasting it into your ``.blackfire.yaml`` file.

This allows you to fine tune this recommendation for your application and adjust
the levels.

But, don't simply disable specific recommendations, as you will lose an
opportunity to improve your application. Tests and recommendations are evaluated
for every profile triggered manually by you, automatically by the monitoring or
with the synthetic monitoring.
