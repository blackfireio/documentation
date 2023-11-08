"sleep()" should not be used during a Web request
=================================================

``sleep()`` might seem convenient to defer the execution of following statements, 
but it has some drawbacks. The most common side effect is timeout: the browser 
doesn't wait for the response and considers it as failed.

Sometimes, ``sleep()`` is used to avoid brute force attacks on wrong password 
attempts. But this process has to rely on a session identifier or an IP address, 
and hackers use browsers without cookie support, and from a lot of IPs.

So ``sleep()`` has no effect in that case and will only result in pausing more
and more execution threads in case of brute force attack, effectively resulting 
into a Denial Of Service attack.

If you want to defer execution, try alternative approaches: `Django Asynchronous Support`_, 
or `AJAX`_.

.. _`Django Asynchronous Support`: https://docs.djangoproject.com/en/3.1/topics/async/
.. _`AJAX`: https://developer.mozilla.org/en/docs/AJAX
