Access Management
=================

.. include-twig:: `youtube-iframe`
    :title: Access Management
    :src: https://www.youtube-nocookie.com/embed/usIksxOZZLY?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

In today's video, we're diving into something crucial for organizing and
securing your projects: :doc:`Blackfire Access Management </up-and-running/access-management/index>`.

We'll explore how to control access effectively across your organization,
environments, and teams. By the end of this video, you should know how to ensure
the right people have the right level of access, and nothing more.

Access management in Blackfire has three main areas:
- :doc:`Organization roles </up-and-running/access-management/organization-roles>`,
- :doc:`Environment access levels </up-and-running/access-management/environment-levels>`,
- and :doc:`Teams </up-and-running/access-management/teams>`.
Let's examine each one in detail.

Organization roles
~~~~~~~~~~~~~~~~~~

First up, let's talk about :doc:`Organization roles </up-and-running/access-management/organization-roles>`.

Organization roles in Blackfire define members' permissions across the entire
:term:`Blackfire Organization <Organization>`. There are four roles available:
**Owner**, **Admin**, **Billing Manager**, and **Member**.

The **owner** has full control over the organization.

This includes managing billing, adding and removing members, and configuring
settings. Each organization has only one owner. It is initially the one who
purchased the Blackfire subscription. If you wish to transfer ownership to someone
else, you need to reach out to our support.

An **Organization Admin** has the same permissions as the owner, but cannot delete
the organization.

The role has been designed so that the owner can delegate responsibilities to
ensure smooth operations at all times.

The **Billing Managers** can manage billing and subscription details and access
invoices.

However, they are not taking any paying seats as they cannot access observability data.

The members have limited permissions and can access organization usage data,
assigned environments and view other members of assigned environments.

Note that members do not take any paying seats unless given access to at least
one environment.

Here you can see how to navigate to the organization settings in Blackfire and
assign roles to new members.

Go to the *Organization Settings*, then *Organization Access Management*, where
you can add new members or adjust their roles using the drop down menu.

Make sure to assign roles based on each person's responsibilities to keep the
organization secure. You can even remove all accesses to someone entirely as
part of the offboarding process.

Environment Access Levels
~~~~~~~~~~~~~~~~~~~~~~~~~

Next, let's discuss environment access levels.

Unlike organization roles which work at a broad level, environment access levels
help you control who can do what within a specific environment. For example, you
might have production and staging environments, each with different access requirements.

There are two levels here, **Contributors** and **Managers**.

**Managers** can manage all aspects of an environment, including settings and access
management.

**Contributors** can use the observability features they have access to and view other
contributors.

To adjust access levels, go to the *Environment Settings*, then
*Environment Access Management*.

You can assign each member a role that best fits their needs.

Note that different environments may require different level of scrutiny. You
probably want fewer managers in production to prevent accidental changes.

Teams
~~~~~

Finally, let's look at **Teams**.

Teams help you group members logically based on projects, roles, and
responsibilities.

This is especially useful when working in large organizations, where not everyone
needs access to every environment. For instance, you may create a backend API
team and assign them access to the Blackfire environment related to their work.

Teams streamline access management by letting you handle permissions collectively
rather than member by member.

Once a team is set up, you can manage their access level at the environment
level, saving you time and reducing errors.

To summarize, effective access management in Blackfire is about assigning the
right roles to the right levels. Use organization roles for broad environment
tasks, environment access levels for more granular control, and teams to simplify
managing groups of people.
