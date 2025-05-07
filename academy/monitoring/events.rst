Mark Events in the Monitoring Timeline
======================================

.. include-twig:: `youtube-iframe`
    :title: Mark Events in the Monitoring Timeline
    :src: https://www.youtube-nocookie.com/embed/xMNcV6cN7A4?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

In this video, we'll explore how to :doc:`add custom markers </monitoring-cookbooks/events>`,
also known as events, to your monitoring and continuous profile timelines.

These markers help provide extra context for what's happening in your application
and infrastructure, such as key user actions, deployment, configuration changes,
or other key actions.

By marking events into your timeline, you can immediately see whether a specific
change correlates with a performance impact. It's a simple way to add valuable
context to your observability data, without cluttering your code or environment.

The way to add an event to the timeline is via a simple cURL command. The body
sent to this endpoint accepts two parameters:

- ``name`` is the label for your event. It takes up to 64 characters and is mandatory.
- ``timestamp`` is an optional valid Unix timestamp to specify the event name.
  If you omit it, Blackfire uses the current time.

Ensure you're targeting the proper Blackfire environment using the drop down
selector. It will automatically fill in the correct credential, so you don't have
to worry about messing up your environment's specific details.

That's how easy it is to add events to your monitoring and continuous profiling
timelines in Blackfire.

By marking critical changes right into your timeline, you'll have richer, more
actionable insights into the performance and behavior of your services.
