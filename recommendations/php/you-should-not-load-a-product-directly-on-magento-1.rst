You should not load a product directly on Magento 1
===================================================

In Magento applications, loading a product directly is a expensive operation
that can slow down the entire application. The reason is that the EAV database
model is used instead of the flat catalog and that requires performing complex
database queries with lots of JOINs.

If you want to load a product, use a collection, look for the product id and
limit the results to just one page of one element, as shown below:

.. code-block:: php

    $productId = 42;
    $product = Mage::getModel('catalog/product')->getCollection()
       ->addFieldToFilter('entity_id', $productId)
       ->addAttributeToSelect(Mage::getSingleton('catalog/config')->getProductCollectionAttributes())
       ->setPage(1, 1)
       ->getFirstItem()
    ;
