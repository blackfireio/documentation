Django DB Persistent Connections should be enabled on production
================================================================

Persistent connections avoid the overhead of re-establishing a connection to 
the database in each request. In Django, the default value is 0, preserving the 
historical behavior of closing the database connection at the end of each request.

To enable persistent connections, set ``CONN_MAX_AGE`` in ``settings.py`` to a 
positive integer of seconds. This defines the maximum lifetime of a connection. 
It can be set independently for each database:

.. code-block:: python

    DATABASES = {
        'default': {
            ...
            'CONN_MAX_AGE': 10, # seconds
            ...
        }
    }

See `Persistent Connections`_ for more information on the subject.

.. _`Persistent Connections`: https://docs.djangoproject.com/en/3.1/ref/databases/#persistent-connections

