Writing Your First Performance Test
===================================

.. include-twig:: `youtube-iframe`
    :title: Writing Your First Performance Test
    :src: https://www.youtube-nocookie.com/embed/9r3BhUVZww?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

By now, you should have a good idea of what performance testing is, and it's
crucial role in future proofing your applications. In this video, we will create
our first performance test using Blackfire.

To start, we need the ``.blackfire.yaml`` file in our project.

If you haven't already created one, Blackfire provides a helpful CLI command to
do it for you.

In a terminal run ``blackfire client:bootstrap-tests`` at the root of your
application. That will create a ``.blackfire.yaml`` file with a basic setup for
your first test.

Let's look at the file we just created. You will see a test named "The homepage
should be fast".

Inside this test, the past key points to forward slash, which is the homepage of
your application. This key supports regular expressions, giving you flexibility
for future tests.

There is only one assertion for our test. The wall-time should be lower than 20
milliseconds. Note that you can create as many tests as you want, containing as
many assertion as you need.

If you scroll down that file a bit more, you might also notice a scenario section
in the same file. This part help you create multi-step performance tests. However,
we will put that aside for now and focus just on the single page tests. We'll
dive deeper into scenarios and synthetic monitoring in a future video.

We have our first test. Let's see what happens when we trigger a profile with
that endpoint, now that we have a test in place

In the deterministic profile UI, you will see an Assertions tab. If your code
meets the requirement, in this example, if the homepage loads in under 20
milliseconds, you will see a green check mark.

Otherwise you will see a warning or failure message letting you know you need to
optimize further.

And that's it. You have created your first test. Congratulations!

Yet this what might not be the best you will ever write. It relies only on the
wall-time, which is a fairly volatile metric. It may be faster if it runs locally
on the new powerful computer, or more likely it'll run slower on your staging
server where too many other dev tools are jamming up the works.

Your next step is to explore how to :doc:`write more detailed and secure assertions <assertions>`
to get even better insights into your code performance.
