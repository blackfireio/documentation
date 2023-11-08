You should enable fast 404 in Drupal 7
======================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by Evolving Web`_.

When an HTTP request is received by Drupal 7, it first checks if the
requested file or directory already exists. If the file or directory
does not exist, then Drupal 7 takes over the request and tries to load
dynamically created content from the database. Hence, for requests
to resources images, audio, video and other media files, if the file
does not exist on the server, the request is sent to Drupal and Drupal
performs expensive tasks of looking up the database for dynamic content
and when no content is found, it renders a 404 page.

For static resource requests, it is easier and way more server-intensive to
check if the requested file has certain extensions like JPG, PNG, GIF, etc and
if the requested file has one of those extensions, then it is possible to
pre-maturely end the request as a 404 without executing the actual Drupal 7
framework.

How To Enable Fast 404
----------------------

Edit your site's ``settings.php`` or ``settings.local.php`` file, which
is usually located in ``sites/default``. Find the line that says:

.. code-block:: php

    # drupal_fast_404();

Uncomment that line and fast 404 should be enabled. You can also install the
`Fast 404 module`_ which provides additional functionality.

.. _`Fast 404 module`: https://www.drupal.org/project/fast_404
.. _`a contribution by Evolving Web`: https://blog.blackfire.io/drupal-7-recommendations.html
