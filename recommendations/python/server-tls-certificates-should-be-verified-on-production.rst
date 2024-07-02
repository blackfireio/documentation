Server TLS Certificates Should Be Verified On Production
========================================================

Most HTTP clients allow to bypass SSL/TLS verification via a special flag. While it
might be acceptable for development purposes, it is insecure for production. Even
if you want it disabled for local testing and development purposes, you might want
to consider using a self-signed certificate.

Bypassing server SSL/TLS verification leaves the requests susceptible to MITM
`(Man-in-the-middle) attacks`_ as it will accept any TLS certificate presented
by the server.

See `SSL certificate verification`_ for ``requests`` library for more information.

.. _`SSL certificate verification`: https://requests.readthedocs.io/en/master/user/advanced/#ssl-cert-verification
.. _`(Man-in-the-middle) attacks`: https://en.wikipedia.org/wiki/Man-in-the-middle_attack
