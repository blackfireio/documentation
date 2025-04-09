Automated Performance Tests [level: Production]
===============================================

.. include-twig:: `youtube-iframe`
    :title: Writing scenarios
    :src: https://www.youtube-nocookie.com/embed/ywxzuaj6nxQ?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Your application's critical user journeys can be protected by assessing their
performance regularly.

Blackfire provides an easy way to describe custom scenarios and when evaluated,
Blackfire will trigger a profile for every URL described in all the steps and
scenarios.

As for all profiles, the matching assertions will be evaluated, and all the
results will be grouped in a convenient report.

Scenarios can be defined in the ``.blackfire.yaml`` file or custom ``.bkf`` ones,
like so:

.. code-block:: yaml

    scenarios: |
        #!blackfire-player

        scenario
                name 'Visitor'

                visit url('/pricing')
                name 'Pricing page'

                visit url('/docs/introduction')
                name 'Documentation'

An `online validator <https://blackfire.io/validator>`_ can help you validate the
syntax of your test files.

.. note::

    :doc:`Explore the possibilities </builds-cookbooks/scenarios>`, such as
    reusing blocks, using variables, including files, and more.
