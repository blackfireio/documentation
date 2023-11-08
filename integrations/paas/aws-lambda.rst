AWS Lambda
==========

Blackfire supports Amazon Lambda for PHP and Python languages.

The Agent
---------

The Blackfire Agent cannot be run in a lambda, and thus needs to be installed
on a separate server, e.g. an Amazon EC2 instance.

An Amazon Machine Image (AMI) can be found in the EC2 community AMI list. You
can find it as *Blackfire.io Agent*.

.. note::

    You may choose a ``t2.micro`` type, as the agent does not need much computing
    power.

Once your instance is started, **take note of its private IP**.
Launch an SSH session and update the system packages using ``apt``. This
ensures that the agent is up-to-date:

.. code-block:: bash

    sudo apt update
    sudo apt upgrade

You then need to :ref:`configure the agent with your Blackfire server
credentials <configuration-agent>`.

.. note::

    The agent is already configured to accept connections from any IP on port
    ``8307``. This is safe as long as port ``8307`` is not accessible from the
    internet. (Only port 22 is accessible from the internet by default.)

Once you have finished configuring the agent, don't forget to restart it:

.. code-block:: bash

    sudo systemctl restart blackfire-agent

PHP Lambda
----------

To deploy PHP Lambdas, we recommend using the `Bref framework
<https://bref.sh>`_, which relies itself on the `Serverless framework
<https://www.serverless.com/>`_.
You may need to follow the `Bref installation documentation
<https://bref.sh/docs/installation.html>`_.

In this context, the Blackfire Probe can be installed with Lambda layers,
provided by the `Bref Extra Extensions repository
<https://github.com/brefphp/extra-php-extensions>`_.

.. code-block:: bash

    composer require bref/extra-php-extensions

Edit the ``serverless.yml`` file:

.. code-block:: yaml

    # ...

    plugins:
        - ./vendor/bref/bref
        - ./vendor/bref/extra-php-extensions # <---- Add the extra Serverless plugin

    functions:
        console:
            handler: public/index.php
            layers:
                - ${bref:layer.php-fpm-81}
                - ${bref-extra:blackfire-php-81} # <---- Add the Blackfire probe

Create the ``php/conf.d/blackfire.ini`` file:

.. code-block:: ini

    extension=/opt/bref-extra/blackfire.so

    ; Replace the following value by your agent IP or domain address.
    blackfire.agent_socket = tcp://ip-172-40-40-40.eu-central-1.compute.internal:8307
    blackfire.agent_timeout = 0.25

And deploy:

.. code-block:: bash

    serverless deploy

Python Lambda
-------------

In Python, the Blackfire Probe is a PIP package, using pre-compiled binaries.
Amazon has a `specific procedure to upload such packages
<https://aws.amazon.com/tr/premiumsupport/knowledge-center/lambda-python-package-compatible/>`_,
but the `Serverless framework <https://www.serverless.com/>`_ can make it
easier by automating everything for you.

Example with Blackfire and Flask:

.. code-block:: bash

    pip install flask
    pip install blinker
    pip install blackfire

    pip freeze > requirements.txt

Edit your ``serverless.yml`` file:

.. code-block:: yaml

    # serverless.yml
    service: serverless-flask
    plugins:
      - serverless-python-requirements
      - serverless-wsgi

    custom:
      wsgi:
        app: app.app
        packRequirements: false
      pythonRequirements:
        dockerizePip: non-linux

    provider:
      name: aws
      runtime: python3.8
      stage: dev
      region: us-east-1

    functions:
      app:
        handler: wsgi.handler
        events:
          - http: ANY /
          - http: 'ANY {proxy+}'
        environment:
          # Change the agent socket to fit yours.
          BLACKFIRE_AGENT_SOCKET: "tcp://ip-172-40-40-40.eu-central-1.compute.internal:8307"
          BLACKFIRE_CLIENT_ID: "<YOUR-BLACKFIRE-CLIENT-ID>"
          BLACKFIRE_CLIENT_TOKEN: "<YOUR-BLACKFIRE-CLIENT-TOKEN>"
          BLACKFIRE_LOG_FILE: /tmp/blackfire_probe.log

And deploy your lambda:

.. code-block:: bash

    serverless deploy
