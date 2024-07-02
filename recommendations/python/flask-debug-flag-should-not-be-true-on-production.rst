Flask DEBUG Flag Should Not Be True In Production
=================================================

Running `Flask in Debug mode`_ is not recommended and should only be used for
local development purposes.

Debug mode exposes information that can be useful to attackers, such as
paths, user details, environment settings, operating system versions and might
allow execution of arbitrary code.

.. _`Flask in Debug mode`: https://flask.palletsprojects.com/en/1.1.x/quickstart/#debug-mode
