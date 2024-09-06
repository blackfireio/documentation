Google Chrome
=============

Using a Web Browser is the easiest way to :doc:`profile web applications
</profiling-cookbooks/profiling-http-via-browser>`. Blackfire supports Google Chrome and
:doc:`Firefox </integrations/browsers/firefox>`.

Installing the Chrome Extension
-------------------------------

.. include-twig:: `companion_chrome_install`

Upgrading the Extension
-----------------------

The Google Chrome extension should be automatically updated by the Google
Chrome Scheduler. However, if a new version is available and your browser
doesn't update it, please follow these steps to force the update:

* Open ``chrome://extensions`` in a new browser tab;
* Check the **Developer mode** at the top right of the screen;
* Click the **Update extensions now** button.

.. include:: _csp.rst

Known limitations
-----------------

.. _profiling-all-requests-chrome:

.. warning::

    The ":ref:`Profile all requests <profiling-all-requests>`" feature is
    currently not available on Chrome as the features conflicts with Chrome
    manifest most recent version (v3).

Whenever the feature is activated, the browser extension triggers profiling by
adding a specific header to all XHR requests, which Chrome manifest v3 prohibits.

Consider using the :doc:`Firefox browser extension </integrations/browsers/firefox>`
to benefit from the ":ref:`Profile all requests <profiling-all-requests>`" feature.
