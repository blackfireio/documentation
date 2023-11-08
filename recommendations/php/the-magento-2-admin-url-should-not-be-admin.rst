The Magento 2 admin URL should not be "admin"
=============================================

For the sake of security, it is recommended to change the default URL to a custom one.
It is highly advised to avoid the default ``admin`` or the commonly used
backend names.
This will help you avoiding determined attackers and reducing exposure to
scripts that try to break into Magento websites.

How To Change This URL
----------------------

Using command line :

.. code-block:: bash

    magento setup:config:set --backend-frontname admin_1wgrah

The ``admin_1wgrah`` string is the new admin URL.
**Define a custom name that fit your needs**

Additional Resources
--------------------

* `Display or change the Admin URI`_ (Magento Developer Documentation)

.. _`Display or change the Admin URI`: https://devdocs.magento.com/guides/v2.3/install-gde/install/cli/install-cli-adminurl.html
