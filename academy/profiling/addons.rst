Blackfire Add-ons
=================

.. include-twig:: `youtube-iframe`
    :title: Blackfire Add-ons
    :src: https://www.youtube-nocookie.com/embed/AvvXBQtFq7s?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

In today's video, we'll examine Blackfire four add-ons in more detail and see
how each other can help you get more out of your deterministic profiling. Those
four add ons are **Quality**, **Security**, **Magento**, and **Debug**.

Quality
~~~~~~~

First up is the **Quality add-on**. It automatically reviews your application
code against our best practice standards. If it detects any flaws, like insecure
coding practices or performance pitfalls, it will immediately flag them. This is
a fantastic way to proactively enforce coding guidelines across your team,
helping everyone maintain a high quality codebase.

Security
~~~~~~~~

Next, we have the **security add-on**, which works similarly by scanning your
profile data for potential vulnerabilities or dependencies with significant
security notices. You will be alerted about any red flags so you can address
them before they become real risks.

Magento
~~~~~~~

The **Magento add-on** is specially crafted for developers using the
:doc:`Magento </php/integrations/magento>` eCommerce platform. It includes
tailored recommendations and checks for Magento specific best practices, making
sure your store runs smoothly, remains secure, and delivers the best possible
experience to your customers.

Finally, there's the Debug add on, which is all about giving you the deepest
insight possible during your development and troubleshooting process.

By default, Blackfire prunes the least significant calls in your profile code
and anonymizes SQL queries and HTTP calls. That's great for privacy and
performance analysis. But, sometimes, you need even more detailed data to
pinpoint a bug.

Debug
~~~~~

When you enable the **debug add-on**, you can disable pruning and anonymization for
specific requests. That way, you will see all function or method calls executed
by your code, and the full SQL arguments, rather than placeholders in your query
list.

Remember never to send personal or sensitive data to Blackfire while profiling
non anonymized requests. This is crucial for complying with privacy best practices.

Note that for prepared SQL statements, arguments are never collected. Only
column names are shown. This feature adds detail to the call graph, not the
timeline.

Enabling Debug Mode is simple. Check the Enable Debugging mode in the browser
extension before running your next profile. Or use the ``--debug`` option with
``blackfire curl`` or ``blackfire run`` to enable the debug mode with the CLI.

To see if you already have access to any of these add ons, or to enhance your
subscription with a new one, head over to your
:doc:`Organization Billing Settings </academy/getting-started/billing>`
page in Blackfire. There, you can manage your plan and add ons to tailor your
Blackfire experience exactly to your needs
