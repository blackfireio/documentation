The Magento 1 config cache should be enabled
============================================

The configuration of a Magento store, including all its modules, is defined in
lots of different XML files. Collecting these files and merging them to generate
the final configuration used by the application consumes lots of resources.

For that reason, Magento includes a special cache to store and reuse the
processed configuration. This cache also contains store-specific settings stored
in the file system and database. Don't forget to clean or flush this cache type
after modifying configuration files.

How To Enable this Cache
------------------------

Using the graphical interface, access the Magento **Admin Panel**, then click on
System > Cache Management and make sure that the **Configuration** status is
**Enabled**.
