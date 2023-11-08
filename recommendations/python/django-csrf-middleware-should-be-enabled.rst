Django CSRF middleware should be enabled
========================================

Cross Site Forgery attack occurs when a malicious website contains a link, a form 
button or some JavaScript that is intended to perform some action on your website, 
using the credentials of a logged-in user who visits the malicious site in their 
browser. `CsrfViewMiddleware`_ adds protection against Cross Site Forgeries by adding 
hidden form fields to POST forms and checking requests for the correct value.

The CSRF middleware is activated by default in the MIDDLEWARE setting. If you 
override that setting, remember that 'django.middleware.csrf.CsrfViewMiddleware'
should come before any view middleware that assume that CSRF attacks have been 
dealt with:

.. code-block:: python

   MIDDLEWARE = [
       ...
       'django.middleware.csrf.CsrfViewMiddleware',
       ...
   ]

For more information, please see: `Cross Site Request Forgery protection`_.

.. _`CsrfViewMiddleware`: https://docs.djangoproject.com/en/3.1/ref/middleware/#django.middleware.csrf.CsrfViewMiddleware
.. _`Cross Site Request Forgery protection`: https://docs.djangoproject.com/en/3.1/ref/csrf/#module-django.middleware.csrf
