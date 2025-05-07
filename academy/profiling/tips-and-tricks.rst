Deterministic Profiles Tips and Tricks
======================================

.. include-twig:: `youtube-iframe`
    :title: Deterministic Profiles Tips and Tricks
    :src: https://www.youtube-nocookie.com/embed/DsOXNhouCeA?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

In this video, we'll explore the deterministic profiling UI and some lesser-known
features that can help you easily identify performance bottlenecks in your
applications.

Blackfire continuous observability isn't just about gathering data, it's about
efficiently navigating and understanding that data.

Let's discover some powerful search and navigation tricks for the deterministic
profile.

Locate SQL queries and HTTP Requests
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When you look at a Blackfire profile, you'll see an overview of all the HTTP
requests and SQL queries your application made during the profile run.

Each one is conveniently displayed in a dedicated tab, letting you drill deeper
into the details.

This is where you can quickly see how many requests were made, how long they
took, and gather insight into the SQL queries that could be slowing down your
app .

A neat trick is that requests and queries are also searchable directly in the
call graph views. You're not limited to searching function names or namespaces.
You can search for specific SQL queries, HTTP requests, or even metrics.

For example, if you copy and paste a SQL query into the search bar, you can
immediately locate the part of your code responsible for running that query.
This is extremely helpful when pinpointing the origin of a slow query.

Search by Namespaces
~~~~~~~~~~~~~~~~~~~~

Another handy shortcut is searching by namespace. This lets you check on the
function calls from your codebase, hiding the activity from your dependencies.

Search by Metric Contribution
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

We can also type ``sql.`` to reveal all function calls contributing to metrics
under the ``sql`` namespace. This help you quickly narrow down the code pass
responsible for SQL activities.

Drill-down Specific Calls
~~~~~~~~~~~~~~~~~~~~~~~~~

When you spot something interesting, maybe a high-cost function, the magnifying
glass icon is your best friend. Clicking on it opens a new version of that call
graph centered on that specific function, letting you remove any clutter and
focus on what truly matters.

You can keep using these magnifying glasses to move around the call graph until
you find exactly what you're looking for.

If you ever need to return to the original view, simply click on the Home icon
at the top right corner.

Indetify Metric Contribution
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Do you notice these colored squares in the function list? They represent each
function's direct contribution to a specific metric.

These color markers help you quickly spot which functions contribute to specific
metrics you want to control better.

Visualize Cache Usage
~~~~~~~~~~~~~~~~~~~~~

Don't forget to check out the cache tab. It's crucial for understanding how your
caches are configured and used.

Are they being hit effectively, or is the cache misconfigured or saturated?

These tabs make it straightforward to identify any issues and fight in your
caching strategy.

Those are our top tips and tricks for navigating the deterministic profiling UI
in Blackfire. With these techniques in hand, you'll be able to fine tune your
application performance faster than ever.
