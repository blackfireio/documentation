Configuring Front-End Observability
===================================

.. include-twig:: `youtube-iframe`
    :title: Configuring Front-End Observability
    :src: https://www.youtube-nocookie.com/embed/9fj-5I_ibek?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

In this video, we will work through how to enable and
:doc:`configure Front-end Observability </front-end-observability/configuration>`
in Blackfire.

You can enable the Front-end Observability features on multiple environments at
once by going to the **Organization settings** > **Front-end usage** in your
Blackfire dashboard.

There you will see a list of all the environments you have access to. With the
right permission, you can enable or disable front-end observability features for
each one. This gives you full control, allowing you to activate it only when
needed.

Each environment also has its own settings. Environment managers can enable or
disable Browser Monitoring and Analytics on that specific environment only.

To collect front-end data, Blackfire uses a JavaScript probe and the unique
browser key. It identifies the environment to which send the front end traces.

If you are using the latest PHP or Python probe, the key is ingested
automatically when the feature is enabled. If you want more control, you can add
those snippets manually to your HTML.

Adding the tracking snippets manually also allows you to add a
``data-transaction-name`` attribute to it, which enables you to explicitly
name transaction.

You will tell me why is naming transaction important. Well, a transaction groups
related request traced by Blackfire. It can represent a controller, an action, a
view, anything meaningful to your application.

When the front end and backend transactions see the same name, Blackfire is
automatically links them.

This lets you navigate seamlessly between front end and backend observability
data.

This way you better understand full stack performance for a given feature and
pinpoint if slowness is set aside.

Front-end observability doesn't have to track every request. You get to choose
the sample rate. That is the percentage of front-end traces to collect.

This helps you balance cost and visibility depending on your traffic, you can
adjust this anytime in your dashboard you can also upgrade your quota or add
one time top-ups.

And that's it. You are now ready to activate front end Observability. Once
enabled, you will start getting real user right in your Blackfire dashboard.
