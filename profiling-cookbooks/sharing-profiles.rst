Sharing Profiles
================

It is possible to share your profiles publicly.

Doing so will result in making it accessible to search engines. Please make sure
not to make public any content that you don't want or are not allowed to share.

Publicly shared profiles benefit from unlimited retention.

We hope that this will help you show the results of your work and write blog
articles to let the rest of the world learn from your expertise. Try embedding
interactive profile views in your articles!

oEmbed
------

Blackfire provides an `oEmbed <https://oembed.com/>`_ endpoint to ease the
integration of Profile graphs on blogs and social media websites.

.. note::

    oEmbed is a format for allowing an embedded representation of a URL on
    third party sites. The simple API allows a website to display embedded
    content (such as photos or videos) when a user posts a link to that
    resource, without having to parse the resource directly.

Any public profile or comparison can be integrated using an oEmbed consumer on
:route:`Blackfire endpoint <oembed_service>` or using the automatic discovery
using the ``<link>`` tags in the graph HTML.

WordPress Configuration
-----------------------

To ease sharing Blackfire public profiles on WordPress version 4.4+, paste
this snippet in the ``functions.php`` file of your theme:

.. code-block:: php

    wp_oembed_add_provider('https://blackfire.io/profiles/*', 'https://blackfire.io/oembed');
