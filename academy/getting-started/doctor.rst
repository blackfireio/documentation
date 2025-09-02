Blackfire Doctor: Installation Troubleshooting
==============================================

.. include-twig:: `youtube-iframe`
    :title: Blackfire Doctor
    :src: https://www.youtube-nocookie.com/embed/OXU1YJJwCXM?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

We have all been there. You install a tool, follow the docs, step by step, maybe
even watch a video tutorial, and then something just doesn't work. Frustrating,
right?

Most of the time, Blackfire installs smoothly with our
:doc:`custom scripts </up-and-running/installation>`. But in those rare, tricky
cases, you might hit a roadblock.

That's where ``blackfire doctor`` comes in. Think of it as your friendly
self-diagnosis tool for Blackfire. Instead of guessing what went wrong, it runs
a complete health check for you.

It reviews the essentials, the Agent, the Probe, your configuration and
connectivity. All the moving parts that needs to work together.

Are the components installed? Are they talking to each other? Can they reach
Blackfire servers? Is the configuration correct? Blackfire doctor gives you the
answers.

Just run one CLI command: ``blackfire doctor``. If everything is good, you will
see green checks across the board. And if something's off ``blackfire doctor``
tells you exactly what and puts you in the right direction.

No more wasting time stressing over setup issues. And if you ever need to reach
out to `our support team <https://support.blackfire.platform.sh/>`_ ,
you can share the doctor report for faster help.
