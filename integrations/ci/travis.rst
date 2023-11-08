Travis CI
=========

`Travis CI <https://travis-ci.com/>`_ is a continuous integration platform for
`GitHub <https://github.com/>`_. If you run your :doc:`PHPUnit tests
</php/integrations/phpunit>` on Travis, read on to learn more about how to
configure it.

First, you need to store the Blackfire client and server credentials so that
Travis has access to them when running Blackfire related tests. By
convention, store them in a ``.blackfire.travis.ini`` file that **you won't
commit in your repository**:

.. code-block:: ini

    ; .blackfire.travis.ini
    [blackfire]

    server-id=<BLACKFIRE_SERVER_ID>
    server-token=<BLACKFIRE_SERVER_TOKEN>
    client-id=<BLACKFIRE_CLIENT_ID>
    client-token=<BLACKFIRE_CLIENT_TOKEN>
    endpoint=https://blackfire.io/
    collector=https://blackfire.io/

Replace the placeholders above with your client and server credentials:

:include_twig:`client_credentials`

:include_twig:`server_credentials`

Then, encrypt the file and commit the encrypted file
(``.blackfire.travis.ini.enc``) to the GitHub repository (replace
``organization/project`` with your GitHub repository name):

.. code-block:: bash

    travis encrypt-file .blackfire.travis.ini -r organization/project

.. caution::

    Note that Travis **does not** allow the decryption of encrypted files on
    GitHub forks, which means that pull requests tests won't have access to the
    Blackfire configuration unless they come from the main repository.

Finally, update your ``.travis.yml`` file to install Blackfire and run the
agent before running the tests according to the following template:

.. code-block:: yaml
    :emphasize-lines: 16,17,18,19,20,21,28,29,30,31,32,33

    language: php

    matrix:
        include:
            - php: 7.3
            - php: 7.4
            - php: 7.4
              env: BLACKFIRE=on

    sudo: false

    cache:
        - $HOME/.composer/cache/files

    before_install:
        - |
            if [[ "$BLACKFIRE" = "on" ]]; then
                openssl aes-256-cbc -K $encrypted_16ab3ffdcd52_key -iv $encrypted_16ab3ffdcd52_iv -in .blackfire.travis.ini.enc -out ~/.blackfire.ini -d
                curl -L https://blackfire.io/api/v1/releases/agent/linux/amd64 | tar zxpf -
                chmod 755 agent && ./agent --config=~/.blackfire.ini --socket=unix:///tmp/blackfire.sock &
            fi

    install:
        - travis_retry composer install

    before_script:
        - phpenv config-rm xdebug.ini || true
        - |
            if [[ "$BLACKFIRE" = "on" ]]; then
                curl -L https://blackfire.io/api/v1/releases/probe/php/linux/amd64/$(php -r "echo PHP_MAJOR_VERSION . PHP_MINOR_VERSION;")-zts | tar zxpf -
                echo "extension=$(pwd)/$(ls blackfire-*.so | tr -d '[[:space:]]')" > ~/.phpenv/versions/$(phpenv version-name)/etc/conf.d/blackfire.ini
                echo "blackfire.agent_socket=unix:///tmp/blackfire.sock" >> ~/.phpenv/versions/$(phpenv version-name)/etc/conf.d/blackfire.ini
            fi

    script:
        - phpunit

.. tip::

    Please update ``$encrypted_16ab3ffdcd52_key`` and ``$encrypted_16ab3ffdcd52_iv``
    with the results of ``travis encrypt-file``.

.. tip::

    To get more accurate results with Blackfire, we highly recommend to disable
    XDebug:

    .. code-block:: yaml

        before_script:
            - phpenv config-rm xdebug.ini || true
