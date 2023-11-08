Chef
====

If you are using `Chef <https://www.chef.io/>`_ on your server infrastructure,
you might want to use the `official Blackfire cookbook
<https://supermarket.chef.io/cookbooks/blackfire>`_ to install the Agent and the
Probe.

.. tip::

    The ``blackfire`` cookbook currently supports all the Linux distributions
    we ship packages for (Debian and RedHat based).

To ease the process of using Blackfire with Chef, define these attributes:

.. code-block:: ruby

    node['blackfire']['agent']['server_id'] = SERVER-ID
    node['blackfire']['agent']['server_token'] = SERVER-TOKEN

From now on, we assume that these attributes are set up properly.

Installation
------------

Install the ``blackfire`` cookbook as usual and include ``blackfire`` in your
node's ``run_list``:

.. code-block:: json

    {
        "name":"my_node",
        "run_list": [
            "recipe[blackfire]"
        ]
    }

You can find information about advanced usages on the `official README
<https://supermarket.chef.io/cookbooks/blackfire#readme>`_.

Debugging the Agent and the PHP Probe
-------------------------------------

By default, the probe is quiet and do not produce logs. To debug problems,
define the following attributes:

.. code-block:: ruby
    :zerocopy:

    node['blackfire']['agent']['log_level'] = '4'
    node['blackfire']['php']['log_level'] = '4'

Automatic Upgrades
------------------

As we ship new versions of Blackfire packages very often, the ``blackfire``
cookbook is configured to update Blackfire's packages automatically at each run.
