Use xrange instead of range for Python 2
========================================

The `xrange`_ function in Python is used to generate a sequence of numbers similar
to `range`_ function. They provide exactly same functionality. The difference is
that ``xrange`` returns a generator that generates the values as you need them
whereas ``range`` returns a ``list`` object that contains all integers which will
use more memory.

The only case where ``xrange`` might be preferred over ``range`` is that if you'd
like to iterate over the list multiple times. Because in that case every integer
will be generated more than once.

.. _`xrange`: https://docs.python.org/2.7/library/functions.html#xrange
.. _`range`: https://docs.python.org/2.7/library/functions.html#range
