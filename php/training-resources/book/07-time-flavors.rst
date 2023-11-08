Chapter 7 - Time Flavors
========================

When talking about performance, time is probably the first dimension everyone
thinks of. Time comes in several flavors, as you discovered when profiling your
first requests. In that chapter we covered several types of time measurements
(wall time, I/O time, and CPU time), but we did not discuss their differences
or unpack why having multiple notions of time is important when analyzing a
profile. The time has come!

Wall Clock Time
---------------

The **Wall Clock Time**, or **Wall Time**, for a function call is the measure of
the *real time* it took to execute its code: the difference between the time at
which the function was entered and the time at which the function ended.

The time it takes to execute some fragment of code depends on the resources it
accesses: the number of instructions executed on the CPU, the amount of data
read from memory, the time it took for network services to respond, the size of
any files read from disk, etc. Each one of these activities incurs some
overhead.

To keep things simple, wall time is usually split in two main parts: the **CPU
Time** and the **I/O Time**.

CPU Time
--------

The **CPU time** is the amount of time the CPU was used for **processing
instructions**.

I/O Time
--------

The **I/O time** is the time the **CPU waited for input/output** (I/O)
operations.

We can divide I/O time into two parts: the **network** and the **disk**.

**Network** activity includes calls to databases like MySQL, PostgreSQL, or
MongoDB; HTTP calls to web services and APIs; calls to cache systems like Redis
and Memcached; communications with services like queues, email daemons, remote
filesystems; etc.

**Disk** activity occurs when a program reads files from the filesystem,
including loading code or files.

.. note::

    Keep in mind that the I/O time is almost never 0 as it includes some
    non-significant activities (like memory access).

CPU vs I/O
----------

In summary:

    Wall Time = CPU Time + I/O Time

    I/O Time = Network Time + Disk Time

Why distinguish these types of times? Well, you've probably heard of a program
being **I/O bound** or **CPU-bound**.

A **CPU-bound** program's speed depends mostly on the CPU. In other words, CPU
utilization is high for long periods of time. The faster the CPU, the faster
the code runs.

On the contrary, an **I/O bound** program's speed is determined by the time
spent waiting for I/O. Faster disks or a faster network improve the overall
performance of I/O bound code.

Being able to understand if a piece of code is CPU intensive or does a lot of
I/O activity is a crucial part of finding the root cause of performance issues
as it gives hints about what to look for.

Inclusive vs Exclusive Time
---------------------------

By now, you should have a clear understanding of the different time
flavors. But as reasoning on the global times is quite useless, Blackfire also
attaches times to each function call. Allocating times is complex, so let's see
how Blackfire does it with a simple example:

.. code-block:: php

    function foo()
    {
        $a = new Bar();
        $count = $a->getCount();

        $str = '';
        for ($i = 0; $i < $count; $i++) {
            $str .= str_repeat('foo', 10);
        }

        $str = $a->sanitizeString($str);

        return $str;
    }

    echo foo();

When calling ``foo()``, a node representing the consumed resources associated
with this call is added in the call graph. The **inclusive time** of this
function call is the time it took to execute all lines of code in the ``foo()``
method.

During the execution of ``foo()``, two methods and one function are called:
``getCount()``, ``sanitizeString()``, and ``str_repeat()``. Those three calls
are represented as **child nodes** in the call graph under the ``foo()``
**parent node**. As discussed in a previous chapter, ``foo()`` has 3
**callees** and ``sanitizeString()`` has one **caller**. And ``getCount()``,
``sanitizeString()``, and ``str_repeat()`` also have their own **inclusive
time**.

The ``foo()`` inclusive time includes the time it takes to execute the code
within the function (like the ``for`` loop) but also the inclusive time for all
its children. That's the reason why it's called the inclusive time.

.. note::

    Blackfire makes no differences between PHP built-in method and function
    calls and userland calls; they are all represented as nodes. However,
    language constructs (like ``for``, ``if``, ...) are not represented as
    nodes.

**The inclusive time allows you to find the critical path of an application.**
When you follow the functions with the highest inclusive time, you are going
down the critical path. The critical path is where you need to look at when
trying to assess an application performance.

What about the exclusive time then?

The **exclusive time** for a function call is the time spent in the function
itself, **excluding time spent in child calls**. The exclusive time for the
``foo()`` function is highlighted in the code below:

.. code-block:: php
    :emphasize-lines: 3,4,6,7,8,9,11,12,13,15,16

    function foo()
    {
        $a = new Bar();
        $count =
            $a->getCount();

        $str = '';
        for ($i = 0; $i < $count; $i++) {
            $str .=
                str_repeat('foo', 10);
        }

        $str =
            $a->sanitizeString($str);

        return $str;
    }

**The exclusive time allows finding the function calls to optimize first.** It
tells you which function calls consumed most of the resources by themselves.

Note that the exclusive/inclusive distinction can be made for all dimensions of
a call graph: the time but also the memory, the network, ...

Conclusion
----------

Time is a complex dimension, but hopefully you now have a better understanding
of the different types of time you will see on a Blackfire call graph.
