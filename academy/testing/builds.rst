Performance Test Automation and CI/CD
=====================================

.. include-twig:: `youtube-iframe`
    :title: Performance Test Automation and CI/CD
    :src: https://www.youtube-nocookie.com/embed/QWTCfvpe3E8?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

By now, you should know how to write :doc:`performance tests </academy/testing/index>`,
and automate them by defining scenarios to secure your critical user journeys.

In today's video, we explore automating even further by automating the
:doc:`Builds </builds-cookbooks/index>` themselves.

You can see it's a big "Start Build" button in the Builds section of your
Blakfire dashboard.

This is the most straightforward way to trigger a Build, when needed.

Periodic Builds
~~~~~~~~~~~~~~~

Below this button, you'll find a section called
:doc:`Periodic Builds </builds-cookbooks/builds-periodic>`.

Here, you can schedule automated Builds to run regularly, like every hour, every
six hours, 12 hours or daily.

This periodic testing is a safety net for your application. It regularly checks
your application's performance, making sure it meets your expectations. This
helps you discover any performance issues early before your users notice them.

CI/CD integration
~~~~~~~~~~~~~~~~~

But we can do even better by preventing performance issues from ever reaching
production. That's what you can achieve by integrating Blackfire Builds or
synthetic monitoring into your CI/CD pipelines.

The first option is to trigger Blackfire Builds programmatically using Blackfire CLI or a cURL request.

In any case, the requirement is to generate a specific Build token from the UI.

Using WebHooks
~~~~~~~~~~~~~~~

Then a new Build can be triggered using the ``blackfire build-trigger`` command
or via ``cURL`` (:doc:`reference </builds-cookbooks/builds-webhook>`)

In both cases, we have the possibility to override the default endpoint. And we
need to provide the ``UUID`` of the BLACKFIRE :doc:`environment </reference-guide/environments>`
in which the Build report has to be sent to, and the token allowing the
operation.

A specific title can also be provided to explain the context in which that Build
was triggered.

The :ref:`documentation <build-webhook-trigger>` provides more information for
all different options.

Comparing Builds
~~~~~~~~~~~~~~~~

There is notably the possibility to define a parent's Build id, which allows for
using :ref:`comparison functions <assertions-comparisons>` when writing assertions.

Yes, you got that right.

You can even write assertion, evaluating the evolution of measurements between
two builds. Therefore controlling the change performance in time.

How powerful is that?

Surely you already know your way to integrate a ``blackfire build-trigger``
command, or a ``cURL`` request as an extra step in your already configure
deployment pipeline.

You could then block the deployment or prevent a pull request from being merged.
We also have integrations with :doc:`GitHub actions </integrations/ci/github-actions>`,
:doc:`Jenkins </integrations/ci/jenkins>`, :doc:`TravisCI </integrations/ci/travis>`,
or Platform-as-a-Service (PaaS) such as :doc:`Platform.sh </integrations/paas/platformsh>`,
:doc:`Upsun </integrations/paas/upsun>`, or :doc:`Adobe Commerce Cloud </integrations/paas/adobe-commerce-cloud>`.

Automation saves you time and helps prevent performance problems before the
reach production.

It keeps your application consistently fast and reliable.

Now you have everything you need to become a Blackfire test suite expert.

Keep testing your application regularly. Improve incrementally your scenarios
and automate your performance testing to ensure your users always have the best
experience possible.
