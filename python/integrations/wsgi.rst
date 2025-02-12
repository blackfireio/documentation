WSGI Middleware [language: Python]
==================================

WSGI (Web Server Gateway Interface) is a specification that defines the protocol
between web servers and Python web applications.

The Blackfire Python SDK contains a middleware easing the integration with WSGI
web applications.

The integrations we provide for :doc:`Django <django>`, :doc:`Flask <flask>`,
:doc:`Odoo <odoo>` are extending the ``BlackfireWSGIMiddleware``. They could
`serve as examples <https://github.com/blackfireio/python-sdk/tree/master/hooks>`_
helping the creation of a new middleware.

Integrations with other frameworks could benefit the Blackfire community. Please
consider :route:`contributing your code <contact-us>`.

Installation
------------

The Blackfire Python SDK is available :doc:`with the Blackfire Python Package
</up-and-running/installation>`.

Configuration
-------------

Create a class extending the ``BlackfireWSGIMiddleware``.

The ``FRAMEWORK`` variable must be set; it should describe the instrumented
application.

.. code-block:: python
    :emphasize-lines: 5

    from blackfire.hooks.wsgi import BlackfireWSGIMiddleware

    class BlackfireFooBarMiddleware(BlackfireWSGIMiddleware):

        FRAMEWORK = 'Foo-Bar'

        ...

Monitoring [level: Production]
------------------------------

A ``get_view_name`` method must be defined to have the requests of your WSGI-based
application be instrumented by :doc:`Blackfire Monitoring</monitoring-cookbooks/index>`.

This function is required only for the monitoring of your application. Its
definition can be omitted if you are not considering it.

The ``get_view_name`` method retrieves the view name executing or handling the
HTTP request. Blackfire Monitoring relies on this information to :doc:`group
requests in the monitoring dashboard</monitoring-cookbooks/naming-transactions>`.

If it returns ``None``, the viewname will be grouped with other :ref:`Unnamed
Transactions<monitoring_unnamed_transactions>`

The function receives 1 parameter:

* ``environ`` is a `dictionary <https://peps.python.org/pep-0333/#environ-variables>`_
  that contains the HTTP request headers and other metadata.

The function should return a ``string`` or ``None``.

.. code-block:: python
    :emphasize-lines: 7

    from blackfire.hooks.wsgi import BlackfireWSGIMiddleware

    class BlackfireFooBarMiddleware(BlackfireWSGIMiddleware):

        FRAMEWORK = 'Foo-Bar'

        def get_view_name(self, environ):
            # implementation ...

Builds [level: Production]
--------------------------

A ``build_blackfire_yml_response`` method must be defined to be able to use
:doc:`Blackfire Builds</builds-cookbooks/index>`.

This function is required only by Blackfire Build. Its definition can be omitted if
you are not considering the Synthetic Monitoring of your application.

This function is called to handle Blackfire builds. When a build ``POST``
request is received, this function gets called to build a framework specific
response that contains the ``.blackfire.yaml`` file contents.

The function receives 4 parameters:

* ``blackfireyml_content``: the content of the ``.blackfire.yaml`` file;

* ``agent_response``: a tuple of values received from the Agent connection when
  the build request is authenticated. ``None`` otherwise. If set, the tuple
  should be sent back as headers in the HTTP response;

* ``environ`` is a `dictionary <https://peps.python.org/pep-0333/#environ-variables>`_
  that contains the HTTP request headers and other metadata;

* ``start_response`` is a `callable <https://peps.python.org/pep-0333/#the-start-response-callable>`_
  used to begin the HTTP response.

The ``build_blackfire_yml_response`` function should return a framework specific
HTTP response.

In the example below, the function returns an instance of ``werkzeug.wrappers.Response``.

In the `Django middleware <https://github.com/blackfireio/python-sdk/blob/master/hooks/django/middleware.py>`_,
it returns an instance of ``django.http.HttpResponse``.

.. code-block:: python

    from blackfire.hooks.wsgi import BlackfireWSGIMiddleware

    class OdooMiddleware(BlackfireWSGIMiddleware):

        FRAMEWORK = 'odoo'

        def build_blackfire_yml_response(
            self, blackfireyml_content, agent_response, environ, start_response
        ):
            from werkzeug.wrappers import Response

            # The .blackfire.yaml file should only be sent for authentified request
            if agent_response:
                return Response(
                    response=blackfireyml_content or '', headers=[agent_response]
                )(environ, start_response)

            return Response()(environ, start_response)
