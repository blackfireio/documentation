Synthetic Monitoring using Scenarios
====================================

.. include-twig:: `youtube-iframe`
    :title: Synthetic Monitoring using Scenarios
    :src: https://www.youtube-nocookie.com/embed/ywxzuaj6nxQ?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

By now, you should have a good understanding on how to create top-notch
individual :doc:`performance tests </academy/testing/index>`.

In today's video, we will see how to test entire part of your application
simultaneously.

We will explore synthetic monitoring, which is the performance test automation
that helps you secure critical user journeys.

Using Scenarios
~~~~~~~~~~~~~~~

With Blackfire, we achieve this by using :doc:`Scenarios </builds-cookbooks/scenarios>`.

**Scenarios** are very useful because they test complete user interactions like
logging in, browsing products, or checking out. They help you ensure the
performance of multiple steps at once.

Here is a basic example of a scenario.

.. code-block:: yaml
    :zerocopy:

    scenarios: |
        #!blackfire-player
        name "Website Pages Check"

        scenario
            visit url("/")
                name "Homepage"
                expect status_code() == 200

            visit url("/product/123")
                name "Product Page"
                expect status_code() == 200

            visit url("/cart")
                name "Shopping Cart"
                expect status_code() == 200

            visit url("/checkout")
                name "Checkout Page"
                expect status_code() == 200


In your ``.blackfire.yaml`` file, you can define multiple steps to visit
different pages.

Behind the scenes, an open source web crawler called Blackfire Player does all
the work. It'll trigger a full profile for each endpoint considered. For all
profiles, the matching assertions are automatically evaluated.

Build Reports
~~~~~~~~~~~~~

The result of all the performance tests are gathered in a convenient view we
call the :doc:`Build Reports </builds-cookbooks/index>`.

In a Build Report, you will find a convenient overview of the passing and
failing tests, all the recommendations associated with each profile.

Define Expectations
~~~~~~~~~~~~~~~~~~~

You can access a specific profile and start your investigation with one click
As we use a :doc:`web crawler </builds-cookbooks/player>`, we can add
:ref:`expectations <writing-expectations>` on top of the assertion you
previously defined.

This could be a specific response code, some body content, or more advanced ones
using the embedded DOM crawler.

Check the :ref:`documentation <writing-expectations>` to discover more
possibilities.

Blackfire player lets you simulate all kinds of requests.

You can define the method of the request, attach a body to it, or specific headers.

You can also request to click on a specific link found in the new previous steps
or submit a form. All those requests as well will be profiled.

Define Secrets and Variables
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can :doc:`define secrets </builds-cookbooks/builds-periodic>` like login
credentials, securely in the Blackfire Build dashboard. This helps you test
applications requiring user login

To go beyond, you can :ref:`define variables <using-variables>` with results
from a previous test and start defining groups, which are reusable parts of
scenarios you can later reassemble as Lego bricks.

You can also :ref:`split your scenarios <organizing-scenarios>` in multiple
``.bkf`` files, you can decide to test individually or combine them all.

Validator
~~~~~~~~~

At `blackfire.io/validator <https://blackfire.io/validator>`_, we provide a
convenient validator for your ``.blackfire.yaml``, and ``.bkf`` files to ensure
they're all correctly formatted.

Scenarios allow you to automate regular checks on your application's performance.

They ensure your critical user journeys always perform well.

By continuously testing these scenarios, you prevent problems before users
experience them.

Your next step is to create your first scenario. A good practice is to add or
improve the scenarios every time you work on a feature.

You can secure your application even more by :doc:`integrating these automated tests
into your CI/CD pipelines <builds>`.
