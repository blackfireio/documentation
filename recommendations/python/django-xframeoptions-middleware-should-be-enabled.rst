Django XFrameOptions middleware should be enabled
=================================================

Clickjacking attack occurs when a malicious site tricks a user into clicking on
a concealed element of another site which they have loaded in a hidden frame or
iframe. ``XFrameOptionsMiddleware`` adds protection against Clickjacking attacks by
setting proper `X-Frame-Options`_ HTTP header in all responses.

Put 'django.middleware.clickjacking.XFrameOptionsMiddleware' to MIDDLEWARE to
enable protection against Clickjacking:

.. code-block:: python

   MIDDLEWARE = [
       ...
       'django.middleware.clickjacking.XFrameOptionsMiddleware',
       ...
   ]

For more information, please see: `Clickjacking Protection`_.

.. _`X-Frame-Options`: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options
.. _`Clickjacking Protection`: https://docs.djangoproject.com/en/3.1/ref/clickjacking/
