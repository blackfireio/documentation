Django Security Middleware Should Be Enabled
============================================

Django Security Middleware provides several security enhancements to the 
request/response cycle. Please see `Django Security Middleware`_ to see the whole
list of security enhancements.

Django Security middleware is activated by default in the MIDDLEWARE setting.

.. code-block:: python

   MIDDLEWARE = [
       ...
       'django.middleware.security.SecurityMiddleware',
       ...
   ]

.. _`Django Security Middleware`: https://docs.djangoproject.com/en/3.1/ref/middleware/#django.middleware.security.SecurityMiddleware
