YAML parsing should be cached in production
===========================================

`YAML`_ is a human-readable data serialization language. In the past years it
has become one of the most widely used formats to write configuration files.

Although YAML files are much leaner than their XML counterparts, parsing them to
generate the PHP structures used by the application takes a non-negligible
amount of time to complete.

To make matters worse, PHP doesn't include built-in support to parse YAML files,
forcing applications to use third-party libraries, such as the ubiquitous
`Symfony YAML component`_.

Considering all this, you should not parse YAML files in production because it
will impact negatively on the application performance. Instead, parse these
files once and cache the result for later reuse.

.. _`YAML`: https://en.wikipedia.org/wiki/YAML
.. _`Symfony YAML component`: https://github.com/symfony/yaml
