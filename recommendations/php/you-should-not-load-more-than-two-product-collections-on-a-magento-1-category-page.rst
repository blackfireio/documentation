You should not load more than two product collections on a Magento 1 category page
==================================================================================

Loading product collections in Magento applications is an expensive operation.
On a category page, loading up to two product collections is reasonable, but
loading more collections will hurt performance.

If you want to augment the loaded collection, add an observer on the
``catalog_block_product_list_collection`` event, which is triggered before the
loading of the collection.

If you want to add some attributes to the collection, you can also include them
in the configuration of your module:

.. code-block:: xml

    <?xml version="1.0" ?>
    <!-- config.xml of your module -->
    <config>
        <!-- ... -->
        <frontend>
            <product>
                <collection>
                    <attributes>
                        <!-- here you can add a lot of nodes, one for each attribute
                             you want to retrieve in your collection -->
                        <code_of_my_attribute />
                    </attributes>
                </collection>
            </product>
        </frontend>
        <!-- ... -->
    </config>
