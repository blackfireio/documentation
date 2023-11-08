The Magento 2 JavaScript bundling should be enabled
===================================================

Magento applications usually enable the *"Merge JavaScript Files"* option to
merge the JavaScript files involved in the rendering of the Magento. However,
this option only merges the JavaScript files declared via layouts and not the
JavaScript files loaded using `RequireJS`_.

For that reason, Magento defines another option called *"Enable Javascript
Bundling"*. If this option is enabled, Magento scans every module directory to
look for JavaScript files. Then, it bundles them all into a single file, which
is the only JavaScript resource loaded by every store page.

How To Enable this JavaScript Bundling
--------------------------------------

1. Go to the **Admin Panel**.
2. Click on the **Stores** menu and then on **Settings** > **Configuration**.
3. On the side menu, click on **Advanced** > **Developer**.
4. Click on the **JavaScript Settings** section to reveal a configuration panel.
5. Make sure that the **Enable Javascript Bundling** value is set to **Yes** and
   save the changes.

Beware that bundling files can produce huge JavaScript files of several
megabytes. If you prefer to generate smaller files, edit the ``view.xml``
configuration and define the list of files to bundle. You can also set the
``js_bundle_size`` option to limit the maximum file size of the bundled
JavaScript file.

.. _`RequireJS`: http://requirejs.org
