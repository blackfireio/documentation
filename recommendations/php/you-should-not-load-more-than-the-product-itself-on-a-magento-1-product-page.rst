You should not load more than the product itself on a Magento 1 product page
============================================================================

By default, when a product is displayed Magento loads all its EAV attributes.
This means that you don't have to load the product again when some element (a
block, a helper, etc.) needs to get some product property. In those cases, you
can use the registry to get the product:

.. code-block:: php

    $product = Mage::registry('current_product');

Moreover, in your code you should pass the product as an argument of your
methods, instead of passing just the product id and looking for the product
repeatedly.

The following example shows what **your code should not do**:

.. code-block:: php

    class Foo
    {
        /**
         * @var Mage_Catalog_Model_Product
         */
        protected $_product;

        /**
         * @param int $productId
         *
         * @return $this
         */
        public function setProduct($productId)
        {
            $this->_product = Mage::getModel('catalog/product')->load($productId);

            return $this;
        }
    }

The following example shows what **your code should do** instead:

.. code-block:: php

    class Foo
    {
        /**
         * @var Mage_Catalog_Model_Product
         */
        protected $_product;

        /**
         * @param Mage_Catalog_Model_Product $product
         *
         * @return $this
         */
        public function setProduct(Mage_Catalog_Model_Product $product)
        {
            $this->_product = $product;

            return $this;
        }
    }
