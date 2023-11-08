Using Unsafe yaml.load Should Be Avoided
========================================

The function ``yaml.load()`` from ``PyYAML`` library is unsafe, as it can potentially 
execute any method from the standard library using the special ``!!`` syntax. 
Although versions greater than ``5.1`` will raise a warning, the function is still not 
deprecated and remains unsafe.

It is recommended to use ``yaml.safe_load()`` function instead.

See `PyYAML yaml.load(input) Deprecation`_ for more information.

.. _`PyYAML yaml.load(input) Deprecation`: https://github.com/yaml/pyyaml/wiki/PyYAML-yaml.load(input)-Deprecation
