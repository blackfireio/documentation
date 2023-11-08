Loading serialized data with Pickle is unsafe
=============================================

Loading serialized data with the pickle module can expose arbitrary code
execution using the **reduce** method.

Attackers might use this flaw to execute arbitrary code on the host by crafting a
custom `__reduce__` method:

.. code-block:: python

    class ShellCode(object):
        def __reduce__(self):
            print('custom code executed!')

Please read the following:
 - `Understanding Python pickling and how to use it securely`_
 - `PyCharm Python Security plugin`_

.. _`Understanding Python pickling and how to use it securely`: https://www.synopsys.com/blogs/software-security/python-pickling/
.. _`PyCharm Python Security plugin`: https://pycharm-security.readthedocs.io/en/latest/checks/PIC100.html
