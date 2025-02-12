Chapter 18 - Crawling and Scraping HTTP Applications
====================================================

In the PHP world, crawling web applications can be done via `Guzzle
<http://guzzlephp.org>`_ or by using a web crawler like `Goutte
<https://github.com/FriendsOfPHP/Goutte>`_, which adds a nice DOM manipulation
layer on top of Guzzle. Functional or acceptance tests for Web applications can
be written via some other Open-Source projects like `Behat
<http://behat.org/>`_ or `Codeception <https://codeception.com/>`_.

Blackfire provides an alternative Open-Source tool that sits between the web
crawling and functional testing spaces: `Blackfire Player
<https://github.com/blackfireio/player>`_. This is an exciting tool that lets
developers define crawling scenarios, set expectations on responses, and of
course run Blackfire assertions against your code. The main advantage of
Blackfire Player over existing solutions is the balance it offers between
native features and the simplicity of writing custom crawlers.

The easiest way to use Blackfire Player is to use the Docker image:

.. code-block:: bash
    :zerocopy:

    alias blackfire-player=docker run --rm -it -e BLACKFIRE_CLIENT_ID -e BLACKFIRE_CLIENT_TOKEN -v "`pwd`:/app" blackfire/player

Then, use ``blackfire-player`` to run the player.

Crawling an HTTP Application
----------------------------

Let's crawl the Finding Bigfoot application by defining a scenario in a
``bigfoot.bkf`` file:

.. code-block:: text

    endpoint 'https://www.book.b7e.io/'

    name 'Finding Bigfoot Scenarios'

    scenario
        name 'Check listing of sightings'

        visit url('/')
            name 'Homepage'
            expect status_code() == 200
            expect header('content_type') matches '/html/'
            expect css('h1').text() matches "/Bigfoot is out there/"

A scenario can have several ``steps`` (like ``visit``, ``click`` or ``submit``),
each one having its own options.

With the ``visit`` step, you must provide a mandatory URL to hit; like ``url('/')``.

Other options used in this example are:

* ``expect``: Some optional expectations on the HTTP response.

* ``name``: The step name.

Run the scenario via the ``blackfire-player`` command line tool:

.. code-block:: bash

    blackfire-player run bigfoot.bkf -vv

The ``-vv`` increases the verbosity of the output and adds some information
about the HTTP interactions with the application:

.. code-block:: text

    Blackfire Player

    Scenario  "Check listing of sightings"
     "Homepage"
    GET https://www.book.b7e.io/
      OK

     OK  Scenarios  1  - Steps  1

If an expectation fails, the scenario is stopped and an error message is
displayed. The command also exits with a status code of ``64`` instead of ``0``:

.. code-block:: text

    Blackfire Player

    Scenario  "Bigfoot is out there"
     "Homepage"
    GET https://www.book.b7e.io/
      Failure on step  "Homepage"  defined in bigfoot.bkf at line  6
      └ Expectation "css('h1').text() matches '/I want to believe/'" failed.
        └ css("h1").text() = "Bigfoot is out there
    "

     KO  Scenarios  1  - Steps  1  - Failures  1

Use ``-vvv`` to make the logs very verbose. This flag adds debug
information to the output.

Running Assertions
------------------

In addition to expectations, the player can also generate profiles and run
assertions defined in the ``.blackfire.yaml`` file. Let's begin by
:ref:`removing time-based assertions <forget-about-time>` in the file defined
:ref:`previously <final-blackfire-yaml>`:

.. code-block:: yaml

    tests:
        "All pages are fast":
            path: "/.*"
            assertions:
                - main.memory < 5Mb

        "Twig displays":
            path: "/.*"
            assertions:
                - metrics.twig.display.count + metrics.twig.render.count < 5

        "Symfony events dispatched":
            path: "/.*"
            assertions:
                - metrics.symfony.events.count < 10

        "Memory evolution":
            path: "/.*"
            assertions:
                - percent(main.memory) < 10%
                - diff(main.memory) < 300kb

We can now run the assertions by passing the ``--blackfire-env`` flag (all
profiles are stored in a build):

.. code-block:: bash

    blackfire-player run bigfoot.bkf --blackfire-env=ENV_NAME_OR_UUID -vv

The output displays the following failed assertion:

.. code-block:: text

    Blackfire Player

    Scenario  "Check first repository"
     "Homepage"
    GET https://www.book.b7e.io/

      Failure on step  "Homepage"  defined in bigfoot.bkf at line  6
      └ Assertions failed:
          metrics.sql.queries.count <= 15
    Blackfire Report at https://blackfire.io/build-sets/2c44ba7d-139b-41ca-b843-a3d1e2763539

     KO  Scenarios  1  - Steps  1  - Failures  1

Now, override the endpoint to ``https://fix2.book.b7e.io/`` via
the ``--endpoint`` flag:

.. code-block:: bash

    blackfire-player run bigfoot.bkf \
    --blackfire-env=ENV_NAME_OR_UUID \
    --endpoint=https://blackfireyaml.book.b7e.io/ \
    -vv

Blackfire assertions should pass and the scenario should end successfully.

By default when using the ``--blackfire-env`` option (which is the case when ran
from our servers), each step is automatically profiled. To disable Blackfire, use
the ``blackfire`` setting:

.. code-block:: text

    visit url('/')
        name 'Homepage'
        blackfire false

Clicking on Links
-----------------

Let's now extend our scenario with a new step to test the *about* page. We can
just ask the player to click on the actual link from the active page:

.. code-block:: text
    :emphasize-lines: 15

    endpoint 'https://bigfoot.demo.blackfire.io/'

    name 'Finding Bigfoot Scenarios'

    scenario
        name 'Check listing of sightings'

        visit url('/')
            name 'Homepage'
            expect status_code() == 200
            expect header('content_type') matches '/html/'
            expect css('h1').text() matches "/Bigfoot is out there/"

        # Click on the About link on the current page.
        click link('About')
            name "Bigfoot about page"
            expect status_code() == 200
            expect css('.col p').text() matches '/We are definitely real "humans"/'

The ``link()`` function finds a link on the current page based on its name. You
can also click on links via CSS selectors:

.. code-block:: text
    :emphasize-lines: 1

    click css('.js-sightings-list > tr:nth-child(3) a')

.. admonition: Blackfire Player Technologies

    Blackfire Player heavily depends on several Symfony Components: `DomCrawler
    <https://symfony.com/doc/current/components/dom_crawler.html>`_,
    `ExpressionLanguage
    <https://symfony.com/doc/current/components/expression_language/syntax.html>`_,
    and `CssSelector
    <https://symfony.com/doc/current/components/css_selector.html>`_. HTTP interactions
    are handled by `Guzzle <http://guzzlephp.org/>`_.

    The ``visit`` and ``expect`` steps expect an expression.

    The ``css()`` and ``xpath()`` functions return the DOM elements matching
    the selector. Both functions return instances of `Symfony DomCrawler
    <https://github.com/symfony/dom-crawler/blob/7.2/Crawler.php>`_
    which give access to many ways to manipulate DOM results.

Values Extraction
-----------------

Now let's rewrite the scenario and remove the hardcoding of links by using
**variable extraction**:

.. code-block:: text
    :emphasize-lines: 6,11

    visit url('/')
        name 'Homepage'
        expect status_code() == 200
        expect header('content_type') matches '/html/'
        expect css('h1').text() matches "/Bigfoot is out there/"
        set sighting_title css('.js-sightings-list > tr:nth-child(3) a').text()

    click css('.js-sightings-list > tr:nth-child(3) a')
        name "Sighting Page"
        expect status_code() == 200
        expect css('h2').text() == sighting_title

The ``set`` option can be used to extract data from the HTTP response (the body
should be HTML, XML, or JSON). The first argument is the variable name, the
second is the value.

Values can be any valid expressions evaluated against the HTTP response. Here,
the name of the first repository listed on the homepage is extracted into the
``repo_name`` variable. This value is then used in the next step to check the
breadcrumb on the project page.

Submitting Forms
----------------

Let's submit the login form as an additional scenario:

.. code-block:: text
    :emphasize-lines: 6,10-11,13

    endpoint 'https://bigfoot.demo.blackfire.io/'

    name 'Finding Bigfoot Scenarios'

    scenario
        name 'Logging in'

        visit url("/login")
            name "Login page"
            set user_login css('form.mb-5 div.pb-2 > code:nth-child(1)').text()
            set user_password css('form.mb-5 div.pb-2 > code:nth-child(2)').text()

        submit button("Sign in")
            name "Authenticate"
            param email user_login
            param password user_password

        follow
            expect css('nav.navbar ul.navbar-nav > li.nav-item:nth-child(3) a.nav-link').text() == ' Log Out'

The credentials are provided in clear in the login page of this demo application.
Notice that we have defined the default values of the ``user_login`` and
``user_password`` variables in the ``set`` options.

Variables can also be defined or overridden via the ``--variable`` CLI flag:

.. code-block:: bash

    blackfire-player run bigfoot.bkf --variable "user_login=foo" --variable "user_password=bar"

Crawling APIs
-------------

Crawling APIs can be done with the exact same primitives. For JSON responses,
use JSON paths in expressions:

.. code-block:: text
    :emphasize-lines: 9,10

    scenario
        name 'Crawling APIs'

        set org_name 'blackfireio'

        visit url('https://api.github.com/orgs/' ~ org_name)
            name 'GitHub Organization data'
            expect status_code() == 200
            expect json('html_url') == 'https://github.com/' ~ org_name
            expect json('type') == 'Organization'

The ``json()`` function extracts data from JSON responses by using JSON
expressions (see `JMESPath <http://jmespath.org/specification.html>`_ for their
syntax).

Scraping Values
---------------

The ``css()``, ``xpath()``, and ``json()`` functions can also be used to scrape
data out of PHP responses via the ``set`` option:

.. code-block:: text
    :emphasize-lines: 10,11

    set repo_name 'blackfireio/symfonycasts-blackfire'

    visit url('https://api.github.com/repos/' ~ repo_name)
        name 'Repository data'
        expect status_code() == 200
        expect json('full_name') == repo_name
        expect json('private') == 0
        expect json('language') == 'PHP'

        # owner.keys(@) is a JMESPath expression
        set owner json('owner.keys(@)')

Store a report of the execution with the extracted values via the ``--json`` flag:

.. code-block:: bash

    blackfire-player run bigfoot.bkf --variable "user_login=foo" --variable "user_password=bar" --json > values.json

The ``values.json`` contains all variables from the scenario run:

.. code-block:: json

        "name": "'Finding Bigfoot Scenarios'",
        "results": [
            {
                "scenario": "'Check listing of sightings'",
                "values": {
                    "sighting_title": "\n            WHAT?' thought Alice to herself, 'Which way? Which way?', holding her hand on.\n        "
                },
                "error": null
            },
            {
                "scenario": null,
                "values": [],
                "error": null
            },
            {
                "scenario": "'Crawling APIs'",
                "values": {
                    "owner": [
                        "login",
                        "id",
                        "node_id",
                        "avatar_url",
                        "gravatar_id",
                        "url",
                        "html_url",
                        "followers_url",
                        "following_url",
                        "gists_url",
                        "starred_url",
                        "subscriptions_url",
                        "organizations_url",
                        "repos_url",
                        "events_url",
                        "received_events_url",
                        "type",
                        "site_admin"
                    ]
                },
                "error": null
            }
        ],
        "message": "Build run successfully",
        "code": 0,
        "success": true,
        "input": {
            "path": "bigfoot.bkf",
            "content": "..."
        }
    }

Conclusion
----------

Blackfire Player is a very powerful Open-Source library for crawling, testing,
and scraping HTTP applications. We have barely scratched the surface of all its
features:

* Several scenarios can be defined in a ``.bkf`` files or in PHP;

* Abstract scenarios to reuse common steps;

* Delays between requests;

* Conditional scenarios execution based on extracted values;

* etc.

You can read Blackfire Player's `extensive documentation
<https://docs.blackfire.io/builds-cookbooks/player>`_ to learn more about all
its features.

Similar to Blackfire Player, there are many other Open-Source libraries that
provide native integrations with Blackfire. The next chapter covers the main
integrations and how you can help us adding more.
