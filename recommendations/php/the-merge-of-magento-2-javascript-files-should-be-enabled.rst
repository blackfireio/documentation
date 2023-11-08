The merge of Magento 2 JavaScript files should be enabled
=========================================================

The dynamic features of the Magento interface are created with several
JavaScript files. Having the JavaScript code scattered across lots of small
JavaScript files is convenient for developers, but it slows down the web page
loading and it hurts the perceived application performance.

Fortunately, the solution to this issue is very simple: instead of loading lots
of small JavaScript files, you can combine their contents into a big single
JavaScript file. Although the amount of data transferred is the same, loading
one file instead of multiple files makes your web pages load greatly faster.

Magento includes a feature called **Merge JavaScript Files** which combines all
the JavaScript files automatically. Make sure that this merging of JavaScript
files is enabled.

How To Enable the Merge of JavaScript Files
-------------------------------------------

1. Go to the **Admin Panel**.
2. Click on the **Stores** menu and then on **Settings** > **Configuration**.
3. On the side menu, click on **Advanced** > **Developer**.
4. Click on the **JavaScript Settings** section to reveal a configuration panel.
5. Make sure that the **Merge JavaScript Files** value is set to **Yes** and
   save the changes.
