Chapter 6 - Installation
========================

Up until now, we have used the Blackfire browser extension to profile a
project hosted on Blackfire servers. This was the easiest way to get us started,
but now it's time for you to use Blackfire on your own projects.

.. note::

    From this chapter on, we will focus on using Blackfire on PHP code. Even
    though the core message is unchanged, you might need to adapt installation
    and usage procedures if you develop
    :doc:`Python applications </up-and-running/installation>`.

Infrastructure
--------------

Blackfire is a SaaS product. The blackfire.io website allows you to manage
your Blackfire project configurations, profiles, and builds. Still, you need
to install some software:

* The **Blackfire PHP C extension**, the probe, instruments PHP code and gathers
  data about runtime behavior. The probe knows how and when to instrument the
  code, and how to extract data out of the PHP runtime.

* The **Blackfire agent** handles most of the intensive operations (like
  cleaning, anonymizing, and compressing the data) before sending each profile
  to Blackfire's servers. It uses a socket to communicate with the probe and
  HTTPS to send data to Blackfire.

When you are manually triggering Blackfire profiles, you will do so using one of
the following tools:

* The **Blackfire browser extensions** make it convenient to generate profiles
  from a browser (Firefox and Google Chrome are supported).

* The **Blackfire client**, which comes bundled with the agent, lets you
  generate profiles from the command line. It gives more flexibility and has
  more features than the browser extensions and will be the covered in a future
  chapter.

.. sidebar:: Data Privacy

    Blackfire servers store some data about your code execution. You can learn
    about data privacy in our :ref:`FAQ <blackfire-data-privacy>` and in this
    `blog post <https://blog.blackfire.io/data-privacy-and-blackfire.html>`_.

Installation on your Local Computer
-----------------------------------

Blackfire is supported on many platforms; install it by following the
:doc:`interactive instructions </up-and-running/installation>` for your
operating system:

Installation on Staging, Testing, and Production
------------------------------------------------

.. note::

  This tutorial can followed along whether you have an active subscription
  or not, as all applications used in this book are publicly profilable.

  You may want to go the :doc:`next chapter <07-time-flavors>` if you don't
  currently have a subscription.

When deploying code to testing, staging, or production environments, you can
use the same installation procedure as in the previous section, or use
Blackfire's integrations with `Chef
<https://docs.blackfire.io/integrations/chef>`_, `Puppet, Ansible
<https://blog.blackfire.io/ansible-puppet-support.html>`_, or `Docker
<https://docs.blackfire.io/up-and-running/docker>`_.

Blackfire is also pre-installed on some platforms, such as `Adobe Commerce
Cloud <https://docs.blackfire.io/php/integrations/magento>`_ or `Platform.sh
<https://docs.blackfire.io/integrations/paas/platformsh>`_. The configuration
procedure might be a little different, please make sure to refer to those
platform's documentation.

Next Steps
----------

You are now ready to profile your very own projects!

First, validate your installation by generating a profile from a browser
extension (`Firefox <https://docs.blackfire.io/integrations/browsers/firefox>`_
and `Google Chrome <https://docs.blackfire.io/integrations/browsers/chrome>`_).
If you have any problems, read our `troubleshooting
<https://support.blackfire.platform.sh/hc/en-us/sections/4792498935058-Troubleshooting>`_
guide or :route:`contact our support <contact-us>`.

Once you're able to generate a profile, use the profiling methodology we
described in the previous chapters to run Blackfire on your applications. I'm
very confident that for any non-trivial codebase, you will find some
optimizations.

Found an optimization? Share it with us on Twitter and use the #blackfireio
hashtag.
