Content Security Policy
-----------------------

The browser extension injects a toolbar in the profiled webpage and uses an
``<iframe>`` to communicate with the probe.

In case the web page declares a `Content Security Policy
<https://en.wikipedia.org/wiki/Content_Security_Policy>`_ regarding frames
usages, the communication may be broken and you would be informed in the toolbar.

In this case, you can declare Blackfire domain as trusted by adding the
``blackfire.io`` domain in your application's headers:

.. code-block:: text

    Content-Security-Policy: frame-src 'self' blackfire.io
