Agent v1 to v2 Upgrade Guide
============================

Agent v2 has a different philosophy and some flags are different. If you are considering
upgrading, here is what you should keep in mind:

A unified Agent and Client
---------------------------

Version 2 brings a unified experience for both the Agent and the Client. As such,
the ``blackfire-agent`` executable does not exist anymore. It has been
replaced by the ``blackfire`` executable.

- The ``blackfire-agent`` command becomes ``blackfire agent:start``.
- The ``blackfire-agent --register`` command becomes ``blackfire agent:config``.
- The ``blackfire config`` command becomes ``blackfire client:config``.

Changes in command-line flags
-----------------------------

- The Verbosity option (``-v``) cannot be used in the form ``-v 4`` (``-v``,
  space, integer). Instead, please use ``-v=4`` (``-v``, equal, integer), or
  ``-v`` / ``-vv`` / ``-vvv``.

- Instead of configuring the previous ``blackfire`` CLI by passing options to
  ``stdin``, you can pass directly the parameters via the command line. ``print
  "foo\nbar\n" | blackfire config`` becomes ``blackfire
  client:config --client-id=foo --client-token=bar``.

- The output on ``stdout`` and ``stderr`` has changed. If you used to pipe the output of
  ``blackfire`` or ``blackfire-agent``, you might have to upgrade your scripts.

  For example, the report of ``blackfire curl`` was previously written on
  ``stdout``, it is now written on ``stderr``.

Docker
------

We provide a new ``2`` tag for the ``blackfire/blackfire`` Docker image that
points to the latest version of the image.

There is also a ``1`` tag alongside the existing ``latest`` tag that points to
the previous version of the image for backward compatibility.
Starting from Sept 1st (end of support of version 1), the ``latest`` tag
will follow version ``2``, and the ``1`` tag will be frozen.

Note that the default port of version ``2`` of the Docker image uses the
``8307`` port instead of ``8707``.
We introduced this change to be consistent with the default port of the
``blackfire`` executable.

Drop of SysVInit in favor of systemd
------------------------------------

We have dropped the ``/etc/init.d/blackfire-agent`` sysvinit script in favor of a
systemd service. The systemd service name stays ``blackfire-agent``. Use these
commands to manipulate the service:

- Use ``sudo systemctl stop blackfire-agent`` to stop the service.
- Use ``sudo systemctl start blackfire-agent`` to start the service.
- Use ``sudo systemctl restart blackfire-agent`` to restart the service.

Windows
-------

We have changed the default Blackfire installation location. It was previously
installed in ``C:\Program Files\Blackfire`` and it is now installed in
``C:\Blackfire``.
