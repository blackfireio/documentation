You should not use deprecated methods on Ibexa view controller
====================================================================

Some of the ViewController methods are deprecated, they are accessible by services named:

- ibexa:viewLocation
- ibexa:embedLocation
- ibexa:viewContent
- ibexa:embedContent

instead of them try to use:

- ibexa:viewAction
- ibexa:embedAction

For more information please read `Content Rendering`_.

.. _`Content Rendering`: https://doc.ibexa.co/en/latest/guide/content_rendering/twig_function_reference/content_twig_functions/#content-rendering
