You should load entities in larger groups in Drupal 8
=====================================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by Evolving Web`_.

Drupal 8 stores most data as **entities**. Types of entity on a site include
nodes, users, tags, views, languages, blocks, files, and more. Each entity
can have a sub-type, and many different fields containing data attached to
the entity.

Entities have to be loaded from the database in order to display data about
them on a page. When an entity is loaded, Drupal must perform many different
database queries to get the data from all the different fields, which is quite
expensive. It turns out, however, that loading multiple entities of the same
type all at once takes only slightly more time than loading a single entity!

You should therefore combine your entity loads, and do as many as possible at
the same time. Most parts of Drupal are already built to do this, for example
a view will load all the relevant entities at once. But custom code has to
be careful to do this in the efficient way.

You should change code that looks like this:

.. code-block:: php

    $nodes = array();
    foreach ($node_ids as $nid) {
      $nodes[] = \Drupal\node\Entity::load($nid);
    }

Instead, it should load all the nodes at once:

.. code-block:: php

    $nodes = \Drupal\node\Entity::loadMultiple($node_ids);


One common way this problem occurs is the *n + 1 query* problem, when iterating
over entities and lazy loading related entities:

.. code-block:: php

  $employees = \Drupal\node\Entity\Node::loadMultiple($employee_ids);
  foreach ($employees as $employee) {
    printf("Manager: %s\n", $employee->field_manager->entity->title->value);
  }

To fix this, you should batch your entity loads:

.. code-block:: php

  $employees = Drupal\node\Entity\Node::loadMultiple($employee_ids);

  // Collect all the IDs of manager nodes.
  $manager_ids = array_filter(array_map(
    function($e) { return $e->field_manager->target_id; },
    $employees
  ));

  // Load all the managers at once.
  $managers = \Drupal\node\Entity\Node::loadMultiple($manager_ids);

  foreach ($manager_ids as $manager_id) {
    printf("Manager: %s\n", $managers[$manager_id]->title->value);
  }

.. _`a contribution by Evolving Web`: https://blog.blackfire.io/drupal8-recommendations.html
