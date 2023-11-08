APCu memory is too fragmented, you should do less deletes or updates
====================================================================

APCu memory model is very friendly to appending new values in shared memory. But
if your application does lots of deletes and updates, then you might end up with
high memory fragmentation.

A highly fragmented memory means that the APCu memory has a high level of empty
memory blocks that aren't big enough to store new values. In fact, for each new
or updated entries, APCu scans the list of small blocks looking for one that is
big enough for the new values.

This process can be high on the CPU. Moreover, the small free blocks cannot be
used for larger values. When no more space is available for some bigger values,
APCu just resets its memory pools, triggering even higher CPU usage, thus
degrading user experience.

Depending on your situation, you might want to use a different cache backend than
APCu, that better fits a high number of deletes or updates. Alternatively, you
might want to increase the APCu memory limit.
