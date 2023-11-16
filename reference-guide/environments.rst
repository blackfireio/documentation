Environments [level: Development/Production]
============================================

What's a Blackfire Environment?
-------------------------------

**It is a collaborative workspace** where to invite collaborators, who are
automatically granted your Edition features and usage level. All profiling
and testing data is shared with the team.

**It is a testing silo** where you write custom metrics according to your
business logic, define tests and their applicability, and where you compare
profiles and iterate.

**It is plugged into your tools and workflow** where you trigger test scenarios,
receive build reports and notifications.

**It lets you manage access to your servers** where you configure at will
the probe, agent, and credentials.

Environments Configuration
--------------------------

Environments configuration include:

 * The ability to add collaborators;
 * The ability to :doc:`start builds </builds-cookbooks/index>`;
 * The ability to :doc:`configure notification channels </builds-cookbooks/notification-channels>`;
 * The ability to :ref:`configure variables <assertions-variables>`;
 * The ability to :ref:`configure the environment's server credentials <configuration-agent>`
   in any machine where Blackfire is installed.

.. note::

    Environments are a very flexible way to profile and test the performance of
    your applications, disregarding the physical machines or VMs. More
    specifically:

    * There's no limit on the number of servers: You can configure the probe
      and agent of a unique Blackfire Environment on multiple servers.
    * There's no limit on the number of projects: The same Blackfire Environment
      can be used to gather data from as many projects as you need
    * There's no limit in the number of webhook endpoints: If you’re a
      Production user, you can start builds using the webhook and have access
      to Platform.sh integrations.
      As an Production user, you have access to all notification channels.
      There’s no limit in an environment’s endpoint configuration, so that with
      the same environment you can execute your test scenarios on different
      domains/sub-domains.

Environment Admin Role
----------------------

The Environment Admin can change the configuration of an Environment. The
Environment Owner can promote an Environment Member to the Admin role or
demote them.

More specifically, the Environment Admin can:

    * Change the environment settings
    * Invite and revoke Environment Members
    * Change the Builds settings (Notifications Channels, Variables, Tested URLs)

And they cannot:

    * Revoke the Environment Owner
    * Promote an Environment Member to Environment Admin
    * Delete the Environment

Example Use Case: Monitoring Production
---------------------------------------

.. raw:: html

    <iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/px_kVnbzNk8?rel=0&showinfo=0&modestbranding=1&autoplay=0" frameborder="0" allow="encrypted-media" allowfullscreen></iframe>
