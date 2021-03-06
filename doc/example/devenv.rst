=======================
Development environment
=======================

tox can be used for just preparing different virtual environments required by a
project.

This feature can be used by deployment tools when preparing deployed project
environments. It can also be used for setting up normalized project development
environments and thus help reduce the risk of different team members using
mismatched development environments.

Here are some examples illustrating how to set up a project's development
environment using tox. For illustration purposes, let us call the development
environment ``devenv``.


Example 1: Basic scenario
=========================

Step 1 - Configure the development environment
----------------------------------------------

First, we prepare the tox configuration for our development environment by
defining a ``[testenv:devenv]`` section in the project's ``tox.ini``
configuration file:

.. code-block:: ini

    [testenv:devenv]
    envdir = devenv
    basepython = python2.7
    usedevelop = True

In it we state:

- what directory to locate the environment in,
- what Python executable to use in the environment,
- that our project should be installed into the environment using ``setup.py
  develop``, as opposed to building and installing its source distribution using
  ``setup.py install``.

Actually, we can configure a lot more, and these are only the required settings.
For example, we can add the following to our configuration, telling tox not to
reuse ``commands`` or ``deps`` settings from the base ``[testenv]``
configuration:

.. code-block:: ini

    commands =
    deps =


Step 2 - Create the development environment
-------------------------------------------

Once the ``[testenv:devenv]`` configuration section has been defined, we create
the actual development environment by running the following:

.. code-block:: shell

    tox -e devenv

This creates the environment at the path specified by the environment's
``envdir`` configuration value.


Example 2: A more complex scenario
==================================

Let us say we want our project development environment to:

- be located in the ``devenv`` directory,
- use Python executable ``python2.7``,
- pull packages from ``requirements.txt``, located in the same directory as
  ``tox.ini``.

Here is an example configuration for the described scenario:

.. code-block:: ini

    [testenv:devenv]
    envdir = devenv
    basepython = python2.7
    usedevelop = True
    deps = -rrequirements.txt
