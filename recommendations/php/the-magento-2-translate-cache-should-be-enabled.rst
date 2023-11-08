The Magento 2 translate cache should be enabled
===============================================

Stores created with Magento can be fully internationalized to translate their
contents and interface into the language of the current visitor. Translations
are defined in CSV files which Magento processes to generate the definitive
contents.

A typical Magento application can include tens of translation files, so
processing all of them consumes lots of resources. For that reason, Magento
includes a special cache to store and reuse the processed translations.

In order to enable this cache, go to the **Admin Panel**, then click on System >
Tools > Cache Management and make sure that the **Translations** status is
**Enabled**.
