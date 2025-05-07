Installation Guide
==================

.. include-twig:: `youtube-iframe`
    :title: Installation Guide
    :src: https://www.youtube-nocookie.com/embed/r_kqmwawfdo?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

By now, you should have a clear picture of the :doc:`components <components>`
needed to collect observability data. In this video, we will work through how to
install them.

To get started, head to the Blackfire documentation. Under the
:doc:`Getting Up and Running </up-and-running/index>` section, look for
:doc:`Installing Blackfire </up-and-running/installation>`. This is your main
reference guide for the entire installation process.

At the top of the page, select the :doc:`Blackfire environment </reference-guide/environments>`
where you want to send your observability data. By picking the correct
**environment** here, the installation snippets will automatically come
prefilled with the appropriate credentials.

Next, You will specify the **infrastructure** you are using, like the Linux
variant, macOS, Windows, and select the language and time that you want to
install. These choices will further tailor the instruction to your setup.

No matter which runtime you choose, the first component to install is always the
Blackfire agent. The agent is a daemon responsible for collecting observability
data from the probe, and communicating with Blackfire servers.

 Follow the instructions provided in the documentation for your specific system.

Note, the agent installation procedure starts by defining environment variables.
Selecting the right Blackfire environment first is important for the process to
work smoothly.

Then, and for PHP and Python, you will need to install the probe for the
deterministic stack of the product. This is a PHP extension and a Python package
responsible for collecting monitoring traces and deterministic profiles.

After installing the agent, check the documentation for
:doc:`Continuous Profiling </continuous-profiling-cookbooks/index>`. This feature
applies to all supported runtimes, giving you ongoing visibility into performance
bottlenecks. You will find a link to the respective continuous profiling
installation and configuration guides.

If you're working with PHP or Python, you can also install the Blackfire
:doc:`browser extensions </integrations/browsers/index>`. These browser extensions
let you :doc:`trigger deterministic profiles directly from your browser </profiling-cookbooks/profiling-http-via-browser>`,
making the profiling process easier and faster.

If you are using :doc:`Docker </up-and-running/docker>`, there is a specific set
of guidelines to help you install both the agent and the probe. Generally
It's best practice in containerized environments to install one Blackfire agent
per node or pod, ensuring reliable coverage across all services.

Blackfire also provides :doc:`integrations </integrations/index>` for some
hosting solutions, such as :doc:`Upsun </integrations/paas/upsun>` or
:doc:`Adobe Commerce Cloud </integrations/paas/adobe-commerce-cloud>`. Be sure
to check out those dedicated pages if you are deploying there.

Lastly, don't forget to configure your :doc:`reverse proxies or CDN </integrations/proxies/index>`.
Make sure any IP filtering includes Blackfire IP addresses, so that data is
always sent and received seamlessly.

You're now ready to install all of the :doc:`Blackfire components <components>`
needed to collect observability data for your applications.

If you run into any issues, check the documentation, or reach out to our support
team at `support.blackfire.io <https://support.blackfire.io>`_.
