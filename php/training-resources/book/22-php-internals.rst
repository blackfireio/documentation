Chapter 22 - Understanding PHP Internals
========================================

Understanding how PHP works goes a long way toward writing performant code.
There are quite a few blogs and presentations online describing PHP internals,
but very few of them are performance oriented. This chapter explains some PHP
behaviors that have a direct impact on performance. This is far from being a
comprehensive list of everything you need to know about how PHP works behind
the scenes, but just an introduction to invite you to learn more about PHP
internals.

.. tip::

    There's no need to understand PHP internals if you are running an old
    version of PHP. Getting performance improvements for free can often be
    achieved by upgrading to the latest PHP version.

Reference Mismatches
--------------------

Reference mismatches happen anytime a **by-value** variable is passed to a
**by-ref** function argument, and the other way around.

.. code-block:: php
    :emphasize-lines: 8

    function foo($arg)
    {
    }

    $a = "some var";

    // This turns $a AND $b into references
    $b = &$a;

    // Reference mismatch
    foo($a);

    // Reference mismatch again
    foo($b);

In this example, function ``foo()`` declares a by-value argument (``$arg``),
but the ``foo($a)`` and ``foo($b)`` calls pass a reference created by line 8.

Because the function signature and the passed arguments mismatch, the PHP
engine has to **duplicate the variable value in memory**, and will destroy it
afterward if the function does not use the variable to send it to other
function calls.

The performance impact depends on the type of the argument: duplicating an
object is easy and fast, but big arrays or large strings are much slower to
duplicate:

.. code-block:: php
    :emphasize-lines: 11

    function foo($data)
    {
        echo "In function: ".memory_get_usage()."\n";
    }

    echo "Initial memory: ".memory_get_usage()."\n";

    $r = range(1, 1024);

    // Create a reference set
    $r2 = &$r;

    echo "Array created: ".memory_get_usage()."\n";

    foo($r);

    echo "End of function: ".memory_get_usage()."\n";

    /*
    Initial memory:  235,664
    Array created:   383,592
    In function:     482,080
    End of function: 383,624
    */

The result of executing the above script is clear, passing a big array to the
``foo()`` function with a reference mismatch raises memory usage during the
time of the function execution (from about 375Kb to 473Kb).

Removing the ``&`` when creating ``$r2`` line 11 fixes the problem and memory
stays stable when running the code again:

.. code-block:: php

    /*
    Initial memory:  235,592
    Array created:   383,400
    In function:     383,432
    End of function: 383,432
    */

Using references is often used as a performance optimization, but this is not
always the case. You can see in this example how creating a reference can
increase memory usage significantly, and memory allocation has a direct impact
on performance.

``foreach`` Behavior
--------------------

Unneeded memory increase is not always related to references. Have a look at
this snippet of code:

.. code-block:: php

    $a = range(1, 1024);
    $b = $a;
    echo memory_get_usage()."\n";

    foreach ($a as $v) {
        if ($v == 1) {
            echo memory_get_usage()."\n";
        }
    }

    echo memory_get_usage()."\n" ;

    /*
    373,936
    472,512
    374,056
    */

No references around, but the ``foreach()`` loop consumes a significant amount
of memory. Calling ``$b = $a`` is very fast as PHP uses copy-on-write (its
``refcount`` is incremented). But when ``foreach()`` receives ``$a``, and
because it accepts a by-value variable, it has to duplicate the value because it
does not know if you are going to modify the iterated value inside the loop.

If the ``refcount`` was one, then no duplication would have to happen in the
``foreach`` loop and memory would not increase.

Now, have a look at the following snippet and try to guess if memory is going
to increase within the ``foreach`` loop:

.. code-block:: php

    $a = range(1, 1024);

    // Create a reference set
    $b = &$a;
    echo memory_get_usage()."\n";

    foreach ($a as $v) {
         if ($v == 1) {
            echo memory_get_usage()."\n";
         }
    }

    echo memory_get_usage()."\n";

If you think memory increases because of the reference set, you are wrong. Here
are the numbers when running the code:

.. code-block:: php

    /*
    373,936
    374,056
    374,056
    */

PHP does not have to duplicate the variable because the content is the same
for all references; the refcount does not even matter.

This example demonstrates how guessing PHP behavior can be quite hard without
understanding how it works. Learning more about PHP references is a good place
to start your lessons.

``__invoke()`` and Dynamic Function Calls
-----------------------------------------

A dynamic call occurs when the function name is stored in a variable:

.. code-block:: php

    $a = 'foo';

    $a();

Most PHP developers know that this is bad for performance. For regular function
calls, PHP computes a string hash **at compilation**, which is then used to
lookup the function at runtime. But for dynamic calls, PHP is forced to make
the same computation **at runtime**. Moreover, functions being case
insensitive, the engine is also forced to ``strtolower()`` the function name
each time you call it.

A few calls do not make a difference, but many calls in a recursive function or
in a loop can have a significant performance impact.

Even for regular function calls, PHP might not optimize the call:

.. code-block:: php

    foo();

    function foo()
    {
    }

Defining a function after using it is perfectly valid, but when the compiler
deals with the ``foo()`` function call, it knows nothing about the ``foo()``
definition as it is not declared yet, so it generates OPCodes that force the
runtime engine to resolve the function call (look it up in a hashtable),
something that can be prevented by moving the function definition above the
function call.

Note that **OPcache automatically optimizes this case for you**.

.. sidebar:: Implementation Details matter

    On the same topic, calling ``__invoke()`` on a closure is slower than
    letting PHP handle it itself:

    .. code-block:: php

        $a = function () {
        };

        $a->__invoke();

    This is because ``__invoke()`` does not exist in the ``Closure`` class, it
    is emulated by reflection. This emulation forces the PHP engine to build
    the internal function call and pass it to the executor. Calling ``$a()``
    does not have this overhead.

    A simple benchmark will show that calling ``__invoke()`` on a closure is
    about twice as slow as a direct invocation.

Realpath Cache Size
-------------------

Every time a PHP script tries to access a file, a directory, or a link, the
operating system must resolve its realpath via the ``lstat()`` system call.
This call is fast, but it involves a context switch with the kernel.

PHP will cache up to 16k of realpath accesses by default, but this cache size
is too small for PHP applications that are composed of thousands of files and
directories. You can increase the cache size by setting the
``realpath_cache_size`` ini setting in ``php.ini``.

But instead of guessing the best value, configure a high value first (``1Mb``),
use ``realpath_cache_size()`` at the end of your application to see how much
cache is used by your application, and adjust the ``php.ini`` value accordingly.

PHP 7 Packed Arrays
-------------------

PHP 7 has been rewritten with performance in mind. A lot of work has been done
to reduce memory allocations and memory usage. One such example is the new PHP
7 "packed array."

When using contiguous integer keys, PHP7 packs the array in memory, to make it
consume less:

.. code-block:: php

    $m = memory_get_usage();

    // Create a packed array of keys from 1 to 1024
    $a = range(1, 1024);

    echo memory_get_usage() - $m;

PHP 5.6 shows a memory usage of about 280Kb for this script, but under PHP 7,
memory usage is about 30Kb, which is roughly ten times less (OPcache optimizes
it even more).

When keys are not integers or contiguous, memory usage rises significantly:

.. code-block:: php

    $m = memory_get_usage();

    // Create a packed array of keys from 1 to 1024
    $a = range(1, 1024);

    // Break the packed array
    $a['a'] = 8;

    echo memory_get_usage() - $m;

On the example above, the array in PHP 7 now uses about 70Kb of memory, which
is more than double what the packed array uses.

Conclusion
----------

As demonstrated in this chapter, knowing how PHP works under the hood helps
understand PHP code performance. Don't draw conclusions too fast though;
measure first.
