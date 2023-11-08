PrestaShop Dev Mode should be disabled on production environment
=================================================================

The developer mode is a convenient way to get details on what is happening on your shop when
working on it to modify a theme, develop a new module or extending core features.
Once enabled, PHP becomes talkative when an issue occurs, the cache is regenerated as soon as you introduce new
classes in the codebase...

These features require more resources to run and aren't used by the customers. Turning it off is
recommended on production environments.

The developer mode on PrestaShop is tied to the `_PS_MODE_DEV_` constant.

.. _`documentation`: http://devdocs.prestashop.com/1.7/scale/optimizations/#7-prestashop-settings
