Upgrading to the Production Edition
===================================

When you subscribe to the Production Edition, you gain access to the following
features:

* :doc:`Collaboration features </reference-guide/environments>`.
* :doc:`Access Management </up-and-running/access-management/index>`.
* :doc:`Real-time Monitoring </monitoring-cookbooks/index>` for both HTTP and
  CLI traffic.
* :doc:`Continuous Profiling</continuous-profiling-cookbooks/index>` for PHP,
  Python, Node.js, and Golang.
* :doc:`Alerting </monitoring-cookbooks/alerting>`.
* :doc:`Automatic Profiling </monitoring-cookbooks/automatic-profiling>`.
* :doc:`Distributed Profiling </profiling-cookbooks/distributed-profiling>`.
* :doc:`Testing automation features </builds-cookbooks/index>`.
* :doc:`Advanced integrations </integrations/index>`.
* :doc:`Notifications </integrations/notifiers/index>`.
* `Security <https://www.blackfire.io/code-security/>`_ and `Quality <https://www.blackfire.io/quality/>`_ Addons included.

Get started with the Production Edition
---------------------------------------

To make to most out of the Production Edition, follow these steps:

1. Configure :doc:`Blackfire environments </reference-guide/environments>`
   based on your workflows, tooling and infrastructure. If you need help,
   :route:`contact Support <contact-us>`.
2. :doc:`Configure access </up-and-running/access-management/index>` to your
   organization and environments.
3. Configure Continuous Profiling for your :doc:`PHP</continuous-profiling-cookbooks/php>`,
   :doc:`Python</continuous-profiling-cookbooks/python>`,
   :doc:`Node.js</continuous-profiling-cookbooks/nodejs/index>`, and
   :doc:`Golang</continuous-profiling-cookbooks/go>` applications.
4. If you have configured Blackfire on a public website, set up :ref:`periodic
   builds <trigger-scheduled>`.
5. Write your first :doc:`tests </testing-cookbooks/tests>`,
   :doc:`scenarios </builds-cookbooks/scenarios>` and :doc:`metrics
   </testing-cookbooks/metrics>`.
6. Learn how to :doc:`trigger builds</builds-cookbooks/index>` using
   :doc:`native integrations </integrations/index>`, :doc:`CI/CD pipelines
   </integrations/ci/index>` and the API (:doc:`PHP </php/integrations/sdk>`
   or :doc:`Python </python/integrations/sdk>`).
7. Set up :doc:`notification channels </builds-cookbooks/notification-channels>`
   for your monitoring alerts and build results.

When you configure :doc:`Blackfire environments </reference-guide/environments>`,
consider where your app is deployed and why. For instance, you can create the
following environments:

* One environment for development. All of your team members can use the
  corresponding server credentials on their machines to benefit from the
  Production Edition features while profiling locally deployed apps.
* One environment for testing/staging. This allows you to
  automatically start Blackfire builds if you have continuous
  integration/continuous development tooling and infrastructure
  configured.
* One environment for production, where you can configure periodic builds and
  get detailed insights into code performance.
  Configure :doc:`Blackfire Monitoring </monitoring-cookbooks/index>` and
  :ref:`periodic builds <trigger-scheduled>` and get live insights into code
  performance where it really matters.
