You should not load more than the product itself on a Magento 2 product page
============================================================================

By default, when a product is displayed Magento loads all its EAV attributes.
This means that you don't have to load the product again when some element (a
block, a helper, etc.) needs to get some product property. In those cases, you
can use the registry to get the product:

.. code-block:: php

    /* Considering:
    * @var $coreRegistry \Magento\Framework\Registry
    *      You can get it using the Dependency Injection of your block's constructor
    */
    $product = $coreRegistry->registry('current_product');

Moreover, in your code you should pass the product as an argument of your
methods, instead of passing just the product id and looking for the product
repeatedly.

The following example shows what **your code should not do**:

.. code-block:: php

    class Foo
    {
        /**
         * @var \Magento\Catalog\Model\Product
         */
        protected $_product;
    
        /**
         * @var \Magento\Catalog\Model\ProductFactory
         */
        protected $_productFactory;
    
        /**
         * Set the product
         * @param int $productId
         * @return $this
         */
        public function setProduct($productId)
        {
            $this->_product = $this->_productFactory->create()->load($productId);
            return $this;
        }
    }

The following example shows what **your code should do** instead:

.. code-block:: php

    use Magento\Catalog\Model\Product;

    class Foo
    {
        /**
         * @var \Magento\Catalog\Model\Product
         */
        protected $_product;
    
        /**
         * Set the product
         * @param Product $product
         * @return $this
         */
        public function setProduct(Product $product)
        {
            $this->_product = $product;
            return $this;
        }
    }
