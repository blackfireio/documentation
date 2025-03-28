Writing great assertions
========================

.. include-twig:: `youtube-iframe`
    :title: Writing assertions
    :src: https://www.youtube-nocookie.com/embed/55McQ8-NAg4?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

At this stage, you should hopefully have a ``.blackfire.yaml`` file containing
your very first test. If not, you can `create one in minutes <https://blog.blackfire.io/getting-started-with-the-blackfire-test-suite-part-1-of-series.html>`_.

You can define as many tests as you need, each containing as many assertions as
required. But, **what makes a good assertion?**

Assertions are based on the available metrics and, as Blackfire provides over
700 metrics and allows you to create your own, there's a lot of choice and
testing available.

To write an assertion on a specific dimension, append the dimension name to the
metric name, separated with a ``.``. For example, if you want to base your
assertion on the number of SQL requests made, append ``count`` to
``metrics.sql.queries``: ``metrics.sql.queries.count``.

The available dimensions are ``count``, ``wall_time``, ``cpu_time``, ``memory``,
``peak_memory``, ``network_in``, ``network_in``, ``io``. Then use main to target
the profile itself, using the same dimensions.

Assertions can also use functions to account for the context. The ``is_dev()``
function returns false in a production environment, and the ``var()`` function
returns the value of a user-defined variable.

.. code-block:: yaml

    tests:
        "Pages shouldn't use too much memory":
            path: "/.*"
            assertions:
                - "main.peak_memory < 10mb * var('memory_coeff', 1)"

.. note::

    :doc:`Dig deeper into the possibilities. </testing-cookbooks/assertions>`
