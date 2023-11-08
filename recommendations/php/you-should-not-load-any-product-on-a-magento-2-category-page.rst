You should not load any product on a Magento 2 category page
============================================================

In Magento applications, loading a product directly is a expensive operation
that can slow down the entire application. The reason is that the EAV database
model is used instead of the flat catalog and that requires performing complex
database queries with lots of JOINs.

If you want to load a product, use a collection, look for the product id and
limit the results to just one page of one element, as shown below:

.. code-block:: php

    /* Considering:
     * @var $productCollectionFactory \Magento\Catalog\Model\ResourceModel\Product\CollectionFactory
     * @var $productId int
     * @var $catalogConfig \Magento\Catalog\Model\Config
     */
    $product = $productCollectionFactory->create()
       ->addFieldToFilter('entity_id', $productId)
       ->addAttributeToSelect($catalogConfig->getProductAttributes())
       ->setPage(1, 1)
       ->getFirstItem()
    ;

Considering you are on a category page, you probably don't have all the attributes
you need in your collection. And that's why you are probably loading your products
again to get what you want.

Loading a product directly results in a full product with all the attributes it has.
But there is `another way to get the attributes you want in your category's products`_.

.. _`another way to get the attributes you want in your category's products`: https://magento.stackexchange.com/questions/120504/what-is-the-equivalent-of-the-config-node-category-collection-attributes-in-mage
