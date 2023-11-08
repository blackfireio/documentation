The Magento 1 layout cache should be enabled
============================================

Magento application implements the `Model-View-Controller architecture pattern`_.
Layouts are the major part of the view layer and they define the page structure
using blocks and containers.

In practice layouts are defined in XML files and any given Magento application
includes tens of layout files for its themes, modules and components. Processing
these files to generate the full page structure consumes lots of resources. For
that reason, Magento includes a special cache to store and reuse the processed
layouts.

How To Enable this Cache
------------------------

Using the graphical interface, access the Magento **Admin Panel**, then click on
System > Cache Management and make sure that the **Layouts** status is **Enabled**.

.. _`Model-View-Controller architecture pattern`: https://en.wikipedia.org/wiki/Model–view–controller
