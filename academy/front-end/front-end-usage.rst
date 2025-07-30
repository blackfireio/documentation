Browser Monitoring & Analytics Usage
====================================

.. include-twig:: `youtube-iframe`
    :title: Browser Monitoring & Analytics Usage
    :src: https://www.youtube-nocookie.com/embed/P_tEGpibqHQ?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

In this video, we'll show you how to
:doc:`monitor and manage your usage of front-end observability features </front-end-observability/front-end-usage>`
in Blackfire.

We want you in the driver seats, always in a position to make educated decisions
on how to use and scale the features you use. You can see how many browser traces
have been collected per environment by going to the
**Organization settings > Browser usage**.

The dashboard gives you a clear breakdown on, how much of your quota has been
consumed day by day across the environments you have access to. Traces from other
environments in your organization are grouped under "other environments".

Now let's talk about **spike protection**.

Let's say your site goes viral or faces a bot attack. Blackfire automatically
detects abnormal traffic spikes to protect your monthly quota.

If the system detects an ingestion rate exceeding 15 times your current quota,
it'll temporarily pause front end data collection for 15 minutes. After that,
it resumes automatically.

This ensures your quota isn't drained by surprise, and your insights continue
without major disruption.

With usage tracking and spike protection, you stay in control of your front-end
observability. You can monitor usage trends, adjust your sampling rate, or
plan your upgrades when needed, all from the same dashboard.
