The Sylius event sonata_block_render_event should not be called, use sylius_template_event instead
==================================================================================================

Since version 1.7, Sylius implements a new template architecture without
Sonata.

A pure Twig implementation is used, no event listeners for increased
performance.

Replace ``sonata_block_render_event`` with ``sylius_template_event``
--------------------------------------------------------------------

In your twig files, search and replace ``sonata_block_render_event`` with
``sylius_template_event``:

.. code-block:: twig

    {{ sonata_block_render_event('sylius.admin.order.show.before_summary', {'resource': resource}) }}

.. code-block:: twig

    {{ sylius_template_event('sylius.admin.order.show.before_summary', {'resource': resource}) }}

Then a block can be injected by configuring UiBundle:

.. code-block:: yaml

    sylius_ui:
        events:
            sylius.admin.order.show.before_summary:
                blocks:
                    some_block: 'template.html.twig' # short syntax
                    another_block: # long syntax
                        template: 'another.html.twig'

See the `New template events architecture`_ issue on GitHub for more
information about the implementation.

.. _`New template events architecture`: https://github.com/Sylius/Sylius/issues/10997
