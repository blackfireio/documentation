Chapter 1 - Introduction
========================

15 years ago, writing unit tests for a project was not a widespread practice in
the PHP world. As a matter of fact, PHPUnit only reached `version 1.0 <https
://sebastian-bergmann.de/archives/300-PHPUnit-1.0.0-Released.html>`_ in
mid-2004. How did we know our projects were bug-free back then? By clicking
around, literally. After fixing a bug, or adding a new feature, developers would
browse their applications like crazy to check that nothing was broken. Needless
to say, this was a tedious, boring, and error-prone process. After a while,
developers and project managers were doing less manual testing and bugs were
"unintentionally" deployed to production servers and regressions were common. In
a way, customers and end-users were in charge of the quality assurance.

Nowadays, everyone writes unit and/or functional tests for their PHP
applications. At least, everyone should as we now have great tools like PHPUnit,
Behat, Codeception, Selenium, and more. If you are not writing tests, you
probably feel bad about it, right?

People don't write tests because it's fun or easy. We write tests because the
**cost of a bug** or a regression is gigantic. A bad user experience has a
direct, negative impact on **business reputation** and damages a company's
**bottom line**. This is nothing new. According to Boehm and Basili's "Software
Defect Reduction Top List" published in 2001, the cost of fixing a bug is **15
times more expensive** after release (from $937 in development to $14,102 in
production).

What about performance? How many developers continuously test the performance of
their applications? According to my own experience, not that many. What's more,
nobody feels ashamed for not writing performance tests; probably because the
existing tools are not good enough. Unfortunately, performance issues have the
same impact as bugs: **bad user experience leading to less engagement and
revenue loss**.

How do you ensure that the performance of your applications is good enough
**before** going to production? Are you using a load-testing tool? Are you
benchmarking your code? How do you find bottlenecks?

We've all used the simple ``microtime()`` PHP built-in function for testing
performance. I've used it myself for many years to try to optimize my PHP
projects. It is frustrating to say the least. ``microtime()`` can only tell you
part of the story: some code takes more time than it should. This is okay, but
it cannot tell you why the code is slow or how you can improve it. Even if you
find a bottleneck, validating a fix is difficult as numbers can vary widely from
one run to the next, and the seemingly innocuous changes can have negative
impacts on other parts of the code.

The point is that it is easy to make stupid performance mistakes: n + 1 queries
when using an ORM is the first one that comes to mind, but they are many other
ones.

.. note::

    The *n + 1 query* problem occurs when getting children records of a main
    record with an ORM. When lazy-loading is enabled, the ORM will get the main
    record from the database and then issue n additional queries for the
    children records; the more children you have, the more queries are issued,
    and the slower the code becomes.

**Performance management** is not something you do once, just before you release
your code. In order to be effective, performance management must be included in
your day-to-day workflow via deep integrations into your development stack.
That is what I'm going to write about in this series.

Good tools go a long way. Some solutions have been around for many years, but
thanks to `Blackfire <https://www.blackfire.io/>`_, many more people are now
optimizing their projects dramatically:

* `trivago: Continuous Performance Monitoring for PHP - The tale of Blackfire at
  trivago <https://tech.trivago.com/post/2017-10-27-blackfire/>`_:
  " Blackfire allowed us to:
  Enforce a backend performance budget to stop continuous performance
  degradation over time;
  Detect performance bottlenecks before they’re deployed to production;
  Offer a common platform for PHP developers to discuss performance related
  issues. "

* `Improving Symfony VarDumper by 30%
  <https://github.com/symfony/symfony/pull/23683/>`_


* `Creatuity: Improving RuralKing's Magento shop
  <https://blog.blackfire.io/creatuity-magento-performance-refactoring.html/>`_:
  SQL time was improved by up to 72% on a critical page of RuralKing's checkout!

* `How we sped up Sylius' Behat suite with Blackfire
  <http://lakion.com/blog/how-did-we-speed-up-sylius-behat-suite-with-blackfire>`_:
  The Sylius test suite is now 6 times faster and consumes 90% less memory!

* `Optimizing league/commonmark with Blackfire.io
  <https://www.colinodell.com/blog/201511/optimizing-leaguecommonmark-blackfireio>`_:
  Two simple changes led to a whopping 52.5% performance boost!

In the next 23 chapters, I will guide you through Blackfire's features and
discuss how you can leverage Blackfire to better test your application's
performance in an automated and continuous way. You will also learn that
Blackfire is not just about performance; it is also a great tool to help you
achieve **better code quality**, **improved security** and **best practices
enforcement**.

But first, why is performance so important?
`According to Google
<https://blog.google/products/admanager/the-need-for-mobile-speed/>`_:
**53% of visits are abandoned if a mobile site takes longer than 3 seconds to load**.
Your customer is gone, probably forever. If your web applications are not fast
enough, you will lose both customers and revenue. That's why performance
optimization is key to success. Ready to learn more?
