Version Lifecycle and Deprecation Policy
========================================

We maintain a **predictable deprecation policy** to ensure you benefit from the
latest security patches, performance improvements, and reliability enhancements.

Core Principles
---------------

- **Predictability**: You'll always know when a version is approaching end-of-life
- **Grace periods**: A minimum 180-day notice before any version becomes unsupported
- **Upstream alignment**: We follow the lifecycle of languages and platforms you already use
- **Empathy over strictness**: Our goal is to help you stay current, not to break your workflows

This policy applies to:

* :term:`Blackfire Probes <Probe>`
* :term:`Blackfire Agent <Agent>`

Versioning and Support
----------------------

Blackfire uses Calendar Versioning (CalVer).

Version numbers ``YY.MM.Patch`` reflect the release date, making the 180-day
support window self-evident.

Blackfire Probes Lifecycle
---------------------------

Blackfire Probes follow a four-stage lifecycle based on **upstream runtime
version support** (see `PHP <https://endoflife.date/php>`_ and,
`Python <https://endoflife.date/python>`_ lifecycles):

- **Active**: Any version currently in upstream active support.
   - These versions receive ongoing maintenance updates.
   - They move to **Deprecated** once upstream ends active support and
     security-only support begins.
- **Deprecated**:
   - The version has reached the end of active support and only receives
     security updates.
   - Version that has reached community EOL but is protected by extended support
     remains **Deprecated**.
- **Retired**: The version has reached community EOL and is not protected by extended support.
   - We stop patching but keep the image available "as-is".
   - **180 days before decommission**
- **Decommissioned**: The Probe could no longer be available for download.

The 180-Day Rule
~~~~~~~~~~~~~~~~

Even if your PHP or Python version is **Active**, specific versions of the
Blackfire Probe expire:

- New Probe versions are released regularly to add features or fix bugs.
- Older versions are **Retired** as soon a new Probe version is released, .
- You have **180 days** from the release of a newer Probe to upgrade before
  older version are **Decommissioned**.

Extended Support Exceptions: PHP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

PHP received **Extended Support** from third parties on :doc:`Upsun </integrations/paas/upsun>`,
which extends the Blackfire Probe lifecycle for all users.

PHP versions that have reached community EOL have their related Probe remain in
the **Deprecated** stage. They are receiving security updates but **new features
might not be backported**.

Once the extended support ends, the Probe will move to **Retired** and eventually
to **Decommissioned** after the 180-day grace period.

.. note::

   We encourage PHP users to always upgrade and stay on supported versions to
   benefit from the latest features and security improvements.

Upgrading Your Probes
~~~~~~~~~~~~~~~~~~~~~

:doc:`Please follow the manual upgrade instructions <update>` to ensure your
Probes are always up to date and secure.

Blackfire Agent Lifecycle
-------------------------

The Blackfire Agent follows a three-stage lifecycle:

- **Active**: The latest Agent released
- **Retired**: Any older version
   - The Agent enters this stage immediately when a newer version is published.
   - **180 days before decommission**
- **Decommissioned**: Binary execution is "best-effort" only
   - It displays upgrade instructions and security/support disclaimers.
   - Use it at your own risk.

.. warning::
   **180-Day Grace Period**: When a new Agent version is released, you have
   **180 days** to upgrade before the previous version is decommissioned.

   Mark your calendar and embed Blackfire in your periodic upgrade workflows.

Upgrading Your Agent
~~~~~~~~~~~~~~~~~~~~

If you installed via a package manager, use the standard
:doc:`update commands <update>`.

If you downloaded the binary directly, use the built-in update ``self:update``
command:

.. code-block:: back

   blackfire self:update

Self-Awareness
~~~~~~~~~~~~~~

The Blackfire CLI includes a built-in self-awareness feature to help you stay current:

* You'll see a friendly reminder to upgrade when running commands with a **Retired** version
* The non-blocking message includes the decommission date and upgrade instructions
