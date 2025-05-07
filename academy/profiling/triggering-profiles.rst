Triggering deterministic profiles
=================================

.. include-twig:: `youtube-iframe`
    :title: Triggering deterministic profiles
    :src: https://www.youtube-nocookie.com/embed/EfRWjkh8C4M?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

In this video, we will explore the many ways of triggering profiles.
:term:`Profiles <Profile>` are the most extensive set of data that Blackfire can
collect. They aim to help you understand why a specific script behaves in a
certain way, and allow you to identify the root cause of bottlenecks to the
function or service call level.

If you haven't done it yet, it's time to :doc:`trigger your first profile </onboarding/profiling/triggering-profiles>`
and collect that data.

Trigger HTTP Profiles
~~~~~~~~~~~~~~~~~~~~~

There are multiple ways to trigger a profile with Blackfire. The first, and
often simplest way to profile an HTTP request is :doc:`via the web browser </profiling-cookbooks/profiling-http-via-browser>`
using the browser extensions for :doc:`Firefox </integrations/browsers/firefox>`
or :doc:`Chrome </integrations/browsers/chrome>`.

Once you have installed the Blackfire browser extension, make sure you are
logged in into Blackfire. Then, simply visit the page you want to profile, and
click on the big red "**Profile!**" CTA.

Behind the scenes, it will trigger a profile to that page, adding a specific
header to the request. The profile will ultimately only be triggered if Blackfire
is correctly set up on that server, and if you have permission to the related
Blackfire :doc:`environment </reference-guide/environments>`.

The Profile All Requests, CTA, has Blackfire profile all async requests, including
POST requests, AJAX requests, and API calls. As of recording, this feature is
only available on Firefox, as Chrome's latest manifest prevents intercepting
requests to add specific headers.

Trigger HTTP Profiles via CLI
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Sometimes, you may need more control over a profile, such as adding custom
headers or testing endpoints without a browser. That's where
:doc:`HTTP profiling via CLI </profiling-cookbooks/profiling-http-via-cli>` comes
in.

The ``blackfire curl`` command allows you to profile any HTTP endpoint in a
deterministic way. Did you know that browsers can give you the curl arguments
and options, like HTTP headers, to use for any web page you browse, including
AJAX requests?

This feature is known as ``copy-as-curl``. The result can be used directly with
the Blackfire CLI to profile requests from the command line.

Profile CLI commands
~~~~~~~~~~~~~~~~~~~~

Finally, you can also :doc:`profile command line scripts </profiling-cookbooks/profiling-cli>` directly with Blackfire. Whether you're running a Python or PHP script, or a
maintenance task, profiling CLI commands help you identify bottlenecks in scripts
that don't involve a web server at all.

To do this, prefix your usual CLI command with ``blackfire run``.

This will execute that script while collecting performance data, then upload
that data to your Blackfire environment. You can apply the same approach to
composer commands, Symfony or Laravel artisan tasks, CLI based workflows.

This method ensures that any heavy task or shell-based operation can be analyzed
and optimized as effectively as your HTTP base requests .

With these techniques, you can efficiently profile any part of your application
and infrastructure.

Your next step is to dive deeper into analyzing profiles and interpreting their
results.
