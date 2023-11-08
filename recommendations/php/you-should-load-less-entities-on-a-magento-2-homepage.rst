You should load less entities on a Magento 2 homepage
=====================================================

The homepage of any Magento store is the most important page. An exceptional
performance for the homepage will positively influence the customer perception
of your store.

For that reason, you should avoid loading too many entities on the homepage.
Some entities will always be loaded in the homepage, such as the default CMS
Page, but you can avoid loading the rest of entities.

The first alternative is to use the server-side cache to load entities just once.
If this cache can't be used, make use of any of these JavaScript techniques:
use the HTML5 browser storage or some cookies to store information; cache the
entire page and use Ajax requests to fill in the private page information.

If your server allows it, use ESI (Edge Side Includes) to fully cache the entire
page and fill in the sections marked as private with the information retrieved
making other requests to the server.
