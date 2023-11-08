The merge of Magento 2 CSS files should be enabled
==================================================

The design of the Magento interface is created with several CSS stylesheets.
Having the CSS contents scattered across lots of small CSS files is convenient
for designers and developers, but it slows down the web page loading and it
hurts the perceived application performance.

Fortunately, the solution to this issue is very simple: instead of loading lots
of small CSS files, you can combine their contents into a big single CSS file.
Although the amount of data transferred is the same, loading one file instead of
multiple files makes your web pages load greatly faster.

Magento includes a feature called **Merge CSS Files** which combines all the CSS
files automatically. Make sure that this merging of CSS files is enabled.

How To Enable the Merge of CSS Files
-------------------------------------

1. Go to the **Admin Panel**.
2. Click on the **Stores** menu and then on **Settings** > **Configuration**.
3. On the side menu, click on **Advanced** > **Developer**.
4. Click on the **CSS Settings** section to reveal a configuration panel.
5. Make sure that the **Merge CSS Files** value is set to **Yes** and
   save the changes.
