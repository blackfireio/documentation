Some Composer dependencies have known security issues and should be upgraded
============================================================================

Your application has Composer dependencies that are known to contain security
vulnerabilities. For the integrity and security of your application, and to ensure
optimal performance, we strongly recommend that you upgrade to safer versions of
these dependencies.

**Recommended actions:**

- list all outdated dependencies with ``composer outdated`` (`composer outdated documentation <https://getcomposer.org/doc/03-cli.md#outdated>`_)
- Composer ``v2.4+`` has a ``composer audit`` command to help you list and identify security
  vulnerability (`composer audit documentation <https://getcomposer.org/doc/03-cli.md#audit>`_)
