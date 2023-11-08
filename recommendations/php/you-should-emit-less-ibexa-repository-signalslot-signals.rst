You should emit less Ibexa repository SignalSlot signals
==============================================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by ibexa.co`_.

The Signal-Slot system provides a means for realizing loosely coupled dependencies
in the sense that a code entity A can react on an event occurring in code entity B,
without A and B knowing each other directly.
This works by dispatching event information through a central third instance, the so called dispatcher.
You can read more at `Signal Slot`_.

.. _`Signal Slot`: https://doc.ibexa.co/en/latest/releases/ez_platform_v3.0/#signalslots
.. _`a contribution by ibexa.co`: https://blog.blackfire.io/ez-platform-recommendations.html
