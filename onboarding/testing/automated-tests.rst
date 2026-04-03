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

Scenarios are written in ``.bkf`` files using the Blackfire Player DSL:

.. code-block:: blackfire

    name "Website Pages Check"

    scenario
        visit url('/pricing')
            name 'Pricing page'
            expect status_code() == 200
            assert metrics.sql.queries.count < 10

        visit url('/docs/introduction')
            name 'Documentation'
            expect status_code() == 200

An `online validator <https://blackfire.io/validator>`_ can help you validate
the syntax of your ``.bkf`` files.

.. note::

    :doc:`Explore the full Player DSL </builds-cookbooks/player>`, including
    reusable blocks, variables, form submission, and more.
