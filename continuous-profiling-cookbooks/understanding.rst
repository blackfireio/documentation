Understanding the differences between deterministic and probabilistic observability
====================================================================================

Blackfire Profiler: Deterministic observability for PHP and Python
___________________________________________________________________

:doc:`Blackfire Profiler </profiling-cookbooks/index>` has a **deterministic**
approach for PHP and Python, meaning it collects an extensive range of metrics
for every instrumented request or script.

The quantity of data and metrics collected differ for every layer of data
Blackfire collects. The way scripts or requests are chosen to be instrumented
also depends on the data layer.

:doc:`Profiles </profiling-cookbooks/index>` are manually triggered by a
Blackfire user, or automatically triggered by
:doc:`Blackfire builds </builds-cookbooks/index>`, the synthetic monitoring
feature that evaluates the performance of critical user journeys.

Meanwhile, :term:`monitoring traces <Trace>` and :term:`extended traces <Extended Trace>`
are based on the :ref:`sample rate <monitoring_sample_rate>`, which is the
percentage of requests that are monitored.

In that matter, :doc:`Blackfire Monitoring </monitoring-cookbooks/index>` offers
a mix of two approaches:

- a **probabilistic** one on how requests are selected to be instrumented;

- a **deterministic** one on how they are monitored, with the instrumentation
  starting at the very beginning of the request and ending with it.

A `blog post <https://blog.blackfire.io/understanding-monitoring-traces-extended-traces-and-profiles.html>`_
provides all the details on the differences and complementarity between
Blackfire's monitoring :term:`traces <Trace>`,
:term:`extended traces <Extended Trace>`, and :term:`profiles <Profile>`.

Continuous Profiling: Probabilistic observability
_________________________________________________

**Probabilistic profiling** involves capturing data intermittently. It collects
information at defined intervals, logging functions or services activated by any
ongoing request or script. This approach provides a more comprehensive view of
your application's performance over time, but certain event nuances may be
overlooked due to the frequency of sampling.

Comparing deterministic to probabilistic profiling is akin to contrasting medical
imaging devices. Asserting that an fMRI is unequivocally better than a PET scan
or ultrasound is a misplaced judgment; each tool has its specific diagnostic
purpose.

You might not know all the details about a specific script. But you will have a
good overview of everything happening at a specific time. Information on shorter
spans starting and ending between two consecutive ticks won't be collected.

Pros and cons
______________

Both approaches have their strengths and weaknesses. One is not better than the
other. It all depends on the instrumented languages and your understanding of
the data.

- **Deterministic profiling**: Its strength lies in precision and facilitating
  meticulous script analysis. But it's resource-intensive, leading to
  considerable overhead and potential data overload, making analysis potentially
  tedious.

- **Probabilistic profiling**: Lightweight and scalable, tailored for holistic
  application oversight. However, its periodic snapshots might miss rapid
  function calls, yielding a not-so-perfect application map.

Deterministic and probabilistic profiling each hold value within the development
process. The former delivers a thorough and detailed view, while the latter
offers a wider, more adaptable perspective. Developers may choose one or even
combine both approaches based on the project's specifics and the issues faced.