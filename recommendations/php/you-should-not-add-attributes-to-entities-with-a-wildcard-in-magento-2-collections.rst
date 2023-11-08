You should not add attributes to entities with a wildcard in Magento 2 collections
==================================================================================

In Magento applications, loading all entity attributes within a collection is
an expensive operation that can slow down the entire application.

For this reason, you should never use the ``addAttributeToSelect('*')`` syntax.
You should instead select the attributes you really need **one by one** by
passing an array to the ``addAttributeToSelect()`` method.

The following example shows what **your code should not do**:

.. code-block:: php

    /** @var \Magento\Catalog\Model\ResourceModel\Product\Collection $collection */
    $collection = $this->collectionFactory->create();
    $collection->addAttributeToSelect('*'); // Here is the bad practice that shouldn't be done.

The following example shows what **your code should do** instead:

.. code-block:: php

    /** @var \Magento\Catalog\Model\ResourceModel\Product\Collection $collection */
    $collection = $this->collectionFactory->create();
    $collection->addAttributeToSelect(['name', 'short_description', 'description']);
