Django DEBUG flag should not be true in production
==================================================

Running `Django in Debug mode`_ is not recommended and should only be used for 
local development purposes.

Debug mode exposes information that can be useful to attackers, such as 
paths, user details, environment settings, operating system versions and might 
consume more memory on some occasions, which would lead to lower performance.

.. _`Django in Debug mode`: https://docs.djangoproject.com/en/3.1/ref/settings/#std:setting-DEBUG
