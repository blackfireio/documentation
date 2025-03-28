Performance Tests
=================

.. include-twig:: `youtube-iframe`
    :title: Introduction to performance testing
    :src: https://www.youtube-nocookie.com/embed/v7Dy7zMZp9Q?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Performance testing is a crucial part of the software development process.

Testing helps ensure that applications can handle the expected workload and user
traffic, and they can identify any bottlenecks or issues before deployment.

Unfortunately, we tend to have (not so good) reasons for not wanting to write
tests.  The reason is usually a lack of time, and those minutes we don't invest
in testing can turn into days of work when a massive performance regression
sneaks its way into production.

To combat this, Blackfire provides an extensive testing suite allowing you to:

- Define expectations for HTTP requests and CLI
- Automatically evaluate assertions with every profile made
- Secure the critical user journey with synthetic monitoring
- Integrate the tests with your CI/CD pipeline

Blackfire helps you proactively identify existing bottlenecks and the
consequences of upcoming changes before they reach production.

Read More on Performance Testing
--------------------------------

.. note::

    Get started with testing your application with
    :doc:`our documentation </testing-cookbooks/index>` and
    `a series of blog posts <https://blog.blackfire.io/getting-started-with-the-blackfire-test-suite-part-1-of-series.html>`_

.. toctree::
    :maxdepth: 1
    :titlesonly:

    index
    Your first test <first-test>
    Writing assertions <writing-assertions>
    Custom metrics <custom-metrics>
    Automated tests <automated-tests>
    Synthetic Monitoring <synthetic-monitoring>
