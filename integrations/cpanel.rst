cPanel
======

If your project is hosted on a server infrastructure that uses `WHM/cPanel
<https://cpanel.com/>`_, integration with Blackfire is possible by following
this chapter's instructions.

Before starting, check with your provider that the Blackfire stack is installed
and enabled on the server. If not, follow the :ref:`administrator procedure
<cpanel-administrator>` or ask your provider to do so.

Then, follow the procedure depending on which EasyApache version is
installed: :ref:`EasyApache 3 <cpanel-user-ea3>` or :ref:`EasyApache 4
<cpanel-user-ea4>` if you want to use different sets of credentials per website.

.. _cpanel-user-ea4:

EasyApache 4
~~~~~~~~~~~~

To configure Blackfire for EasyApache 4, go to the `MultiPHP INI Editor
<https://documentation.cpanel.net/display/ALD/MultiPHP+INI+Editor+for+cPanel>`_
*(Home >> Software >> MultiPHP INI Editor)*, switch to "Editor Mode", select
the proper domain, and then copy/paste/adapt to your needs the following snippet:

.. code-block:: ini

    [blackfire]
    ; Adapt the following credentials using the ones found on
    ; https://blackfire.io/my/settings/credentials or your environment settings.
    blackfire.server_id=e0b30241-a25d-4162-9ebb-329f784f1fc7
    blackfire.server_token=3ac2260e038f138a5bca515b72c0205117d886777cf6472b14beabb704e06aa1

.. _cpanel-user-ea3:

EasyApache 3
~~~~~~~~~~~~

To configure Blackfire for EasyApache 3, define some environment variables by
creating or editing the ``.htaccess`` file in the project's document root:

.. code-block:: text

    <IfModule mod_env.c>
        # Adapt the following credentials using the one found on
        # https://blackfire.io/my/settings/credentials or your environment settings.
        SetEnv BLACKFIRE_SERVER_ID e0b30241-a25d-4162-9ebb-329f784f1fc7
        SetEnv BLACKFIRE_SERVER_TOKEN 3ac2260e038f138a5bca515b72c0205117d886777cf6472b14beabb704e06aa1
    </IfModule>

.. note::

    If Blackfire has been installed but **not** enabled for all users, enable it
    by creating a custom ``php.ini`` configuration file.

    Create a ``php.ini`` file in your home directory, copy/paste the content of
    the default PHP configuration (usually found at ``/usr/local/lib/php.ini``)
    and append the following content:

    .. code-block:: ini

        [blackfire]
        ; Only required if Blackfire is not loaded for all websites
        extension=blackfire.so

    Then, adapt ``.htaccess`` to use the custom ``php.ini`` file by adding the
    following:

    .. code-block:: text

        <IfModule mod_suphp.c>
            suPHP_ConfigPath /home/<myuser>/php.ini
        </IfModule>

.. caution::

    Some of these steps may not be allowed by your provider. In such a case,
    contact its support and ask for the configuration by pointing at this
    documentation.

.. _cpanel-administrator:

Administrator Procedure
-----------------------

As a cPanel administrator, if you want to provide the Blackfire stack to your
users, you need to install the Agent and the Probe.

To install the stack, you first need to :route:`create an account on
Blackfire.io <signup>`.

Then follow the :doc:`installation instructions </up-and-running/installation>`
for **RedHat** based distributions.

Then, follow the specific procedure for :ref:`EA3 <cpanel-administrator-ea3>`
or :ref:`EA4 <cpanel-administrator-ea4>`.

.. sidebar:: Cluster setup

    If you are managing a cluster setup, please refer to our :ref:`Load
    Balancer section <configuration-load-balancer>` to learn more about the
    various options at your disposal.

.. _cpanel-administrator-ea3:

EasyApache 3
~~~~~~~~~~~~

To enable Blackfire for your users, go to the `PHP Configuration Editor
<https://documentation.cpanel.net/display/ALD/PHP+Configuration+Editor>`_,
switch to "Advanced Mode" and add ``blackfire.so`` to the ``extension`` field.

.. _cpanel-administrator-ea4:

EasyApache 4
~~~~~~~~~~~~

Blackfire should have been automatically enabled by our Redhat package. You can
check by running ``/opt/cpanel/ea-php56/root/usr/bin/php --ri blackfire``
(tweak to match the installed PHP versions).

.. tip::

    Starting with cPanel 68 and Blackfire probe 1.19.0, the next step is not
    required anymore. You only need to follow it if you did not upgrade yet.

Next, allow your users to add Blackfire settings to their ``php.ini``. Edit
``/usr/local/cpanel/whostmgr/etc/phpini_directives.yaml`` and append the
following snippet at the end of the file:

.. code-block:: yaml

    blackfire.server_id:
      changeable: PHP_INI_ALL
      default: NULL
      multiple: 0
      note: 'Blackfire probe Server ID'
      section: 'blackfire'
      type: string
    blackfire.server_token:
      changeable: PHP_INI_ALL
      default: NULL
      multiple: 0
      note: 'Blackfire probe Server Token'
      section: 'blackfire'
      type: string
    blackfire.log_level:
      changeable: PHP_INI_ALL
      default: 1
      multiple: 0
      note: 'Blackfire probe log verbosity level'
      section: 'blackfire'
      type: integer
    blackfire.log_file:
      changeable: PHP_INI_ALL
      default: NULL
      multiple: 0
      note: 'Blackfire probe log destination file'
      section: 'blackfire'
      type: string

.. caution:: **cPanel Updates**

    Currently, because of a cPanel limitation, this last step must be repeated
    on every cPanel upgrade.

    cPanel is aware of this limitation and we are currently in discussion with
    their team to smooth this experience soon.

Uninstall Blackfire
~~~~~~~~~~~~~~~~~~~

If you are using EA3, go to the `PHP Configuration Editor
<https://documentation.cpanel.net/display/ALD/PHP+Configuration+Editor>`_,
switch to "Advanced Mode" and remove ``blackfire.so`` from the ``extension``
field.

In all cases, remove the installed Blackfire packages.
