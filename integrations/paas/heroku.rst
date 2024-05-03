Heroku
======

Blackfire provides an `official buildpack for Heroku
<https://github.com/blackfireio/integration-heroku>`_. This
buildpack lets you configure and use the Blackfire Agent and the Blackfire CLI
Tool. **It is complementary to other builpacks**, such as official language
support buildpacks provided by Heroku.

Install
-------

Configure the Blackfire credentials from your project root directory:

.. include-twig:: `heroku_configuration`

.. note::
    You may use your Blackfire *personal server credentials* or
    :doc:`environment server credentials </reference-guide/environments>`.

Add the Blackfire buildpack to your project:

.. code-block:: bash
    :zerocopy:

    heroku buildpacks:add --index=1 https://github.com/blackfireio/integration-heroku

.. note::

    Blackfire being part of the default PHP buildpack, if you are using PHP
    you don't need to add the Blackfire buildpack. :ref:`Read more details
    below <heroku-php>`.

.. note::

    As `documented in Heroku devcenter
    <https://devcenter.heroku.com/articles/using-multiple-buildpacks-for-an-app#adding-a-buildpack>`_,
    when using multiple buildpacks, the buildpack for the primary language of
    your app should be the last one added.

.. _heroku-php:

**PHP**

Blackfire is part of the default `Heroku PHP buildpack
<https://elements.heroku.com/buildpacks/heroku/heroku-buildpack-php>`_.

To enable Blackfire when using the PHP official Heroku buildpack, add it as a
requirement in the project's ``composer.json`` file:

.. code-block:: bash
    :zerocopy:

    composer require ext-blackfire

.. _heroku-python:

**Python**

Install the Blackfire Probe by referring ``blackfire`` as dependency in your
``requirements.txt`` file, e.g.:

.. code-block:: bash

    blackfire
    django
    jinja2
    gunicorn

Configuration
-------------

To set your config vars, you may use ``heroku config:set`` command.
You may also define them in your app dashboard, in the *Settings* tab.

.. warning::
    Each time you set or update a config var, **you must
    redeploy your app on Heroku**, using a ``git push heroku master``.

Mandatory Config Vars
~~~~~~~~~~~~~~~~~~~~~

The following configuration vars **must be set**:

- ``BLACKFIRE_SERVER_ID``
- ``BLACKFIRE_SERVER_TOKEN``
- ``BLACKFIRE_CLIENT_ID``
- ``BLACKFIRE_CLIENT_TOKEN``

Optional Config Vars
~~~~~~~~~~~~~~~~~~~~

- ``BLACKFIRE_LOG_LEVEL``
- ``BLACKFIRE_COLLECTOR``
- ``BLACKFIRE_AGENT_SOCKET``

Find more details in :ref:`Blackfire Agent configuration documentation
<configuration-agent-envvars>`.

Logs
----

Log files are located in your app at ``/app/.blackfire/var/log``.

Profile
-------

Profile using the regular :doc:`Blackfire CLI </up-and-running/installation>`
tools or a browser (:doc:`Firefox </integrations/browsers/firefox>` or :doc:`Chrome
</integrations/browsers/chrome>`).
