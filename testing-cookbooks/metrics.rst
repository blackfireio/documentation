Metrics
=======

A **metric** is a collection of costs (memory, network, CPU, ...) associated
with some function calls. Blackfire offers some built-in metrics, but you can
also create your custom metrics.

You can define the performance expectations of your projects by setting an
expected **metric value**, on a given metric dimension, in :doc:`assertions
<assertions>`. To write an assertion on a specific dimension, append the
dimension name to the metric name, separated with a ``.``.

For instance, for the ``sql.queries`` metric, the number of calls is stored in
the ``metrics.sql.queries.count`` and the memory usage in
``metrics.sql.queries.peak_memory``. To check that you don't have more than 10
SQL queries in an assertion, you would write ``metrics.sql.queries.count <= 10``.

The available dimensions for metrics are the following ones.

.. include-twig:: `dimensions`

.. _metrics-built-in-metrics:

Built-in Metrics
----------------

.. include-twig:: `builtin_metrics`

.. _metrics-custom-metrics:

Custom Metrics
--------------

By default, Blackfire gives access to a large number of built-in metrics, most
of them being specific to the language or popular Open-Source libraries. Based
on project requirements, custom metrics can also be defined for a project.

Custom metrics can be defined in a :ref:`.blackfire.yaml file
<tests-blackfire-yaml>`. They consist in a block under the ``metrics`` key:

.. code-block:: yaml

    metrics:
        markdown_to_html:
            # Short label for humans
            label: 'Markdown to HTML'

            # Longer description for humans
            description: 'Metric for Markdown to HTML conversion'

            matching_calls:
                php:
                    -
                        callee: "=App\\Utils\\Markdown::toHtml"

.. note::

    Custom metrics can also be defined using the :ref:`PHP SDK
    <php-sdk-custom-metrics>`.

Besides the identifier (``markdown_to_html``), a metric must be associated with
function calls, via a :ref:`metric selector <metrics-selectors>`, e.g.
``=App\Utils\Markdown::toHtml``.
:ref:`Several function selectors are available and described below
<metrics-selectors>`.

To apply stricter constraints, you may combine ``caller`` and
``callee`` in a single block:

.. code-block:: yaml

    metrics:
        markdown_to_html:
            matching_calls:
                php:
                    -
                        caller: "=App\\Twig\\AppExtension::markdownToHtml"
                        callee: "=App\\Utils\\Markdown::toHtml"

Caller/callee groups are always considered **combined with a boolean AND**.

You may chain several blocks of call selectors for a given metric. In that
case, these blocks are **combined with a boolean OR**:

.. code-block:: yaml

    metrics:
        markdown_to_html:
            matching_calls:
                php:
                    # Each matching call contributes to the total cost of the metric.
                    -
                        caller: "=App\\Twig\\AppExtension::markdownToHtml"
                        callee: "=App\\Utils\\Markdown::toHtml"
                    -
                        callee: "=App\\Utils\\AlternativeMarkdown::toHtml"

.. _metrics-selectors:

Defining a Metric Selector
~~~~~~~~~~~~~~~~~~~~~~~~~~

Defining a metric is all about selecting a sub-set of the profile function
calls. A selector first character defines how to interpret the rest of the
expression:

* ``=``: Matches the expression exactly;
* ``|``: Similar to ``=``, but matches any object that is an instance of the class;
* ``^``: Matches everything starting with the expression;
* ``/``: Interprets the expression as a regex that should match;
* ``!``: Interprets the expression as a regex that should not match.

The second part of the selector defines which function calls to match.

Here are some selector examples:

* ``=Class::method``: Matches the ``method`` function calls on ``Class``;

* ``=func``: Matches the ``func`` function calls;

* ``|Psr\Log\LoggerInterface::log``: Matches any calls to ``log`` on objects
  that are an instance of ``Psr\Log\LoggerInterface``;

* ``^ArrayObject::``: Matches all function calls from the ``ArrayObject`` class;

* ``^exif_``: Matches all function calls for which the function starts with
  ``exif_``;

* ``/^Class::(method1|method2)$/``: Matches ``method1`` and ``method2`` calls
  from ``Class``;

* ``!^spl_autoload_call$!``: Matches any function/method calls but
  ``spl_autoload_call`` ones.

.. _metrics-capturing-arguments:

Capturing Arguments
~~~~~~~~~~~~~~~~~~~

Besides matching nodes, a metric can also be used to aggregate function calls
by arguments.

Blackfire aggregates all function calls into one node to make it easy to
reason about resources it consumed. But sometimes, being able to have
**different nodes for a function call depending on one or multiple arguments**
can help if the arguments make the function behave very differently (e.g. a
database function call which is very sensitive to the SQL statement
to be executed).

.. note::

    Arguments are displayed in the Call Graph and in the Timeline views.

.. caution::

    Arguments capturing only works with the ``=`` (`equals`) selector.

When defining arguments capturing, you need to determine:

* Which argument(s) to capture with a **1-based index**.

  If the captured argument is a hash map, you may match a specific key:
  ``1.some_key``;

* The selector for each argument to capture.
  All :ref:`metric selectors listed above <metrics-selectors>` can be used,
  except ``|``.

  Also, the following selectors are available:

  * ``~``: Means *empty value* (or any value representing *empty*).

    This selector can be combined with any of supported selectors, meaning
    *empty or selector*.

    For example, ``~=`` means *empty or specified value* (e.g. ``~=foo``
    means "empty or with ``foo`` string).

    Another example is ``~^http``, meaning *empty or beginning with "http"
    string*.

.. note::

    Captured arguments are converted into strings by the probe. As such, only
    string representations are considered:

    * Booleans are converted to ``true`` or ``false`` strings;

    * Arrays are converted to ``[]`` string;

    * Objects are converted to their FQCN, e.g. ``App\Foo\Bar``.

    Captured arguments being strings, ``|`` cannot apply as a selector.

.. tip::

    As Blackfire displays separate nodes for each unique argument, it is also a
    great way to better understand how the code behaves (for instance, one node
    per event for an event dispatcher handle method instead of one big node for
    all events).

Examples
""""""""

Consider the following class:

.. code-block:: php

    namespace App\Utils;

    class Greetings
    {
        public function phrase(string $greeting, string $extra): string
        {
            usleep(500000);
            return sprintf('%s %s', $greeting, $extra);
        }
    }

**Single argument capture**

.. code-block:: yaml

    metrics:
        greetings:
            label: Greetings phrases
            matching_calls:
                php:
                    - callee:
                          selector: "=App\\Utils\\Greetings::phrase"
                          argument:
                              # Using "*" as a "catch-all" selector generates
                              # a different node per argument
                              1: "*"

In this example, ``$greeting`` argument is captured and therefore discriminates
e.g. *Hello* from *Hi* greetings.

**Multiple arguments capture**

.. code-block:: yaml

    metrics:
        greetings:
            label: Greetings phrases
            matching_calls:
                php:
                    - callee:
                          selector: "=App\\Utils\\Greetings::phrase"
                          argument:
                              # Using Regexp selector.
                              1: "/^(Hello|Hi)/"
                              2: "*"

In this example, ``$greeting`` and ``$extra`` arguments are both being captured.
Different nodes per arguments combination are generated in the callgraph.

**Hash map argument capture**

Now consider that ``phrase()`` method accepts a hash as an argument:

.. code-block:: php

    namespace App\Utils;

    class Greetings
    {
        public function phrase(array $greeting): string
        {
            usleep(500000);
            return sprintf('%s %s', $greeting['greetings'], $greeting['phrase']);
        }
    }

.. code-block:: yaml

    metrics:
        greetings:
            label: Greetings phrases
            matching_calls:
                php:
                    - callee:
                          selector: "=App\\Utils\\Greetings::phrase"
                          argument:
                              # Capture is based on hash map keys.
                              1.greetings: "/^(Hello|Hi)/"
                              1.phrase: "*"

In this example, the capture is based on the hash map keys.
``1.greetings`` means "value from ``greetings`` key of the first argument",
assuming this argument is an actual hash map.

**Named (or keyword) arguments capture**

It is possible to capture arguments by their names with the following languages:

- **Python:**

.. code-block:: python

    def greeting_phrase(greeting, extra=""):
        return f'{greeting} {extra}'

    greeting_phrase(greeting='Hello', extra='World')


.. code-block:: yaml
    :emphasize-lines: 10,11

    metrics:
        greetings:
            label: Greetings phrases
            matching_calls:
                python:
                    - callee:
                          selector: "=greeting_phrase"
                          argument:
                              # Capturing kwargs
                              greeting: "*"
                              extra: "*"

- **PHP (>=7.0):**

.. code-block:: php

    function soup(string $vegetable, string $spice = 'no spice', string $cheese = 'no cheese'): string {
        usleep(1000);
        $recipe = "Making soup with $vegetable, $spice and $cheese";

        return "$recipe\n";
    }

    echo soup('carrot', 'saffron', 'kiri');
    echo soup('cucumber', 'mint');
    // Using PHP 8 named arguments.
    echo soup(cheese: 'gruyere', vegetable: 'onion');

.. code-block:: yaml
    :emphasize-lines: 8,9,10

    metrics:
        soup:
            label: My Yummy Soup
            matching_calls:
                php:
                    - callee:
                        selector: '=soup'
                        argument:
                            vegetable: '*'
                            spice: '*'

Using Custom Metrics in Assertions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Custom metrics can be used in assertions like any other metrics: the name is
made of the ``metrics.`` prefix, then the metric name (``cache.write`` in our
example), and it ends with one of the available dimensions (``.peak_memory`` in
the example):

.. code-block:: yaml

    "metrics.cache.write.peak_memory < 10mb"

.. note::

    As a matter of fact, built-in metrics are defined in the exact same way as
    custom ones.

.. _custom-metrics-timeline:

Using Custom Metrics in the Timeline View
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In the timeline view, all captured metrics are displayed as blocks,
positioned with time offsets. In the left pane, all metrics are listed and
split into 2 groups: ``Metrics`` and ``Other Metrics``.

``Metrics``, on the top, gather *featured* metrics which are called
**Layers**. These layers can result from a combination of different metrics,
e.g. ``markdown`` being a global layer composed of ``markdown.parse.parsedown``,
``php_markdown.parse.parsedown``, and ``commonmark.parse.parsedown``.

``Other Metrics`` represent every other metrics which have been captured.

To add your metrics to the timeline, you need to set the
``timeline`` option to ``true``:

.. code-block:: yaml

    metrics:
        markdown_to_html:
            label: 'Markdown to HTML'
            layer: ~
            timeline: true
            matching_calls:
                php:
                    -
                        callee: "=App\\Utils\\Markdown::toHtml"

The example above adds the ``markdown_to_html`` metric to the timeline
view. Setting ``layer`` to ``~`` makes this metric to be considered as a
layer itself.

.. _timeline-markers-metric:

Adding Markers
""""""""""""""

It is possible to add :ref:`Timeline Markers <timeline-markers>` directly from a
metric, avoiding using the Probe SDK.

In the following example, each time the ``App\Utils\Markdown::toHtml`` is called,
a marker with the label *Markdown to HTML* is added to the timeline.

.. code-block:: yaml

    metrics:
        markdown_to_html:
            label: 'Mardown to HTML'
            marker: 'Markdown to HTML Timeline Marker'
            matching_calls:
                php:
                    -
                        callee: "=App\\Utils\\Markdown::toHtml"

When using :ref:`argument capturing <metrics-capturing-arguments>`, it is
possible to interpolate the argument's value within the marker label:

.. code-block:: yaml

    metrics:
        greetings:
            label: 'Markdown to HTML'
            # Interpolates the value of the first argument in the marker label.
            marker: 'Greetings - ${1}'
            matching_calls:
                php:
                    -
                        callee:
                            selector: "=App\\Utils\\Greetings::phrase"
                            argument:
                                1: "*"

Defining Layers
"""""""""""""""

The trick to defining a new layer is to declare it and reference it to itself in
the ``layer`` key. The following example shows how to define layers in order to
group metrics under them:

.. code-block:: yaml

    metrics:

        # Main layer, will gather dimensions from all attached metrics.
        markdown:
            label: "Markdown"
            # Self referencing metrics are layers.
            layer: markdown
            timeline: true

        # Sub-layer
        markdown.parse:
            label: "Markdown Parser"
            layer: markdown

        markdown.parse.parsedown:
            label: "Markdown Parser (erusev/parsedown)"
            # The layer this metric contributes to.
            layer: markdown.parse
            matching_calls:
                php:
                    - callee: "=Parsedown::text"

        php_markdown.parse.parsedown:
            label: "Markdown Parser (dflydev/markdown)"
            # The layer this metric contributes to.
            layer: markdown.parse
            matching_calls:
                php:
                    - callee: "=dflydev\\markdown\\MarkdownParser::transform"
                      caller: "!^dflydev\\\\markdown\\\\MarkdownParser::transformMarkdown!"
                    - callee: "=dflydev\\markdown\\MarkdownParser::transformMarkdown"

Specifying the Contribution Type of a Metric
""""""""""""""""""""""""""""""""""""""""""""

By default, all dimensions are contributed for each metric. It is however
possible to specify if a given call contributes for its cost, its count, or a
combination of both. These contribution types are displayed when hovering a
metric name in the timeline view.

This can be specified in the ``contrib`` key for each matching call block.
Available values are:

* ``count+cost``: The default value; gathers both count and cost dimensions;

* ``count-only``: Makes the function call contribute its number of calls only;

* ``cost-only``: Makes the function call contribute its cost dimensions only.

.. code-block:: yaml

    metrics:
        markdown_to_html:
            label: 'Markdown to HTML'
            layer: ~
            matching_calls:
                php:
                    -
                        callee: "=App\\Utils\\Markdown::toHtml"
                        contrib: count-only

Full Metrics DSL
~~~~~~~~~~~~~~~~

.. code-block:: yaml

    metrics:
        # Prototype
        metric_identifier:
            label:                ~
            description:          ~
            layer:                null
            timeline:             null
            matching_calls:
                php:
                    contrib:              count+cost # One of "count+cost"; "cost-only"; "count-only"
                    caller:
                        selector:             []
                        argument:             []
                    callee:               # Required
                        selector:             []
                        argument:             []
