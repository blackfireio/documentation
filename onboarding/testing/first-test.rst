Writing your first performance test
===================================

Blackfire's tests are defined in a ``.blackfire.yaml`` :doc:`file </testing-cookbooks/tests#the-code-blackfire-yaml-code-file>`
located at the root of your application.

If this is not yet the case, create one with the following command:
``blackfire client:bootstrap-tests``

And, just like that, you have your first test!

.. code-block:: yaml

    tests:
        "The homepage should be super fast":
            path: "/"
            assertions:
                - "main.wall_time < 20ms"

``path`` can be defined using a regular expression. CLI commands can also be
tested using the ``command`` key instead.

You can define as many tests as you need, each containing as many assertions as
required. All the metrics and dimensions are :doc:`documented </testing-cookbooks/metrics>`.

It is good practice to write tests on the cause of performance, not its
consequences. Tests on time or memory consumption can be volatile, leading to
false negatives.

Basing the tests on reliable metrics such as the number of SQL queries made,
entities hydrated, or the number of calls to greedy functions can be an efficient
and reliable approach to ensure long-term performance improvement.

With that in mind, we can improve our first test by describing why our homepage
is fast:

.. code-block:: yaml

    tests:
        "The homepage should be super fast":
            path: "/"
            assertions:
                - "metrics.sql.queries.count < 15"
                - "metrics.http.requests.count == 0"


