Browser Monitoring
==================

.. include-twig:: `youtube-iframe`
    :title: Introduction to Browser Monitoring
    :src: https://www.youtube-nocookie.com/embed/haPjWc2rZXU?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

In today's video, we will explore :doc:`browser monitoring </front-end-observability/browser-monitoring>`,
a core feature of Blackfire's front-end observability.

Browser monitoring provides visibility to how real users experience websites.
It captures real world data, from real browsers, not synthetic tests.

You will track five key performance metrics. Let's break them down:

- **T.T.F.B., or Time to first bite**: this is how long the browser waits before
  receiving the first bite of data from your server.

  Lower is better. Aim under 200 milliseconds
- **F.C.P. or First Contentful Paint**: this is when something first appears on
  screen: text image logo. It shows the start of a visual feedback. A good FCP
  is under 1.8 seconds.
- **L.C.P. or Largest Contentful Paint**: This measures when the main content
  like a hero image or headline, finishes loading.

  It tells users the page is mostly here. Aim for under 2.5 seconds.
- **C.L.S. or Cumulative Layout Shift**. This tracks how much the page jumps
  around while loading.

  A low score means a stable layout. Try to keep CLS below 0.1
- **I.N.P., or Interaction to Next Paint**. This shows how quickly your site
  reacts to user input. Lower is smoother. I.N.P. should be under 200
  milliseconds for most interactions.

Each metric reveals something different about the user experience: when content
appears on the screen? How stable the language remains, as the page loads, and
how fast the site feels when user try to interact with it?

If even one of this is off, your users will feel it.

Browser monitoring also shows you geographic performance. You can quickly see
where users are struggling.

The geographic map helps you prioritize improvement by showing you where
performance issues are most concentrated.

Each metrics links directly to Blackfire full stack view.

Click on the slow L.C.P. and you can see the backend trace that contributed to
it. No more jumping between tools

And just like for all of Blackfire, Browser Monitoring is privacy-first.

It does not track individuals, store cookies or collect any personally
identifiable information or P.I.I.. This means you don't need cookie banners.
Your setup is GDPR-compliant by default, and user consent flow remains
completely unaffected.
