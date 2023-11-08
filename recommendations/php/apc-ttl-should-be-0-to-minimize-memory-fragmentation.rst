"apc.ttl" should be 0 to minimize memory fragmentation
======================================================

In the event of running out of available memory, the APCu cache will be
completely expunged when ``apc.ttl`` is equal to 0. This is the recommended
setting because this clearing strategy is the most efficient one in terms of CPU
and memory fragmentation.

When the TTL is greater than 0, when storing new entries, APC will attempt to
remove expired entries based on their last-access time. While this strategy allows
filling up the cache memory to higher levels, it can create high memory
fragmentation and can be very CPU intensive, effectively destroying the benefit
of the caching layer.
