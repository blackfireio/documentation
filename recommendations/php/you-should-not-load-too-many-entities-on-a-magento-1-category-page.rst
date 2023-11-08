You should not load too many entities on a Magento 1 category page
==================================================================

The category pages of any Magento store are one of the most used navigation
elements. An exceptional performance for those pages will positively influence
the customer perception of your store.

For that reason, you should avoid loading too many entities on the category
pages. The first alternative is to use the server-side cache to load entities
just once. If this cache can't be used, make use of any of these JavaScript
techniques: use the HTML5 browser storage or some cookies to store information;
cache the entire page and use Ajax requests to fill in the private page
information.

If your server allows it, use ESI (Edge Side Includes) to fully cache the entire
page and fill in the sections marked as private with the information retrieved
making other requests to the server.
