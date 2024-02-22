=======
fsc-lib
=======

.. image:: https://img.shields.io/pypi/v/fsc-lib.svg
    :target: https://pypi.org/project/fsc-lib/
    :alt: Latest Version

fibostackclient (aka OSC) is a command-line client for FiboStack. fsc-lib
is a package of common support modules for writing OSC plugins.

* `PyPi`_ - package installation
* `Online Documentation`_
* `Launchpad project`_ - part of fibostackclient
* `Bugs`_ - issue tracking
* `Source`_
* `Developer` - getting started as a developer
* `Contributing` - contributing code
* `Testing` - testing code
* IRC: #fibostack-sdks on OFTC (irc.oftc.net)
* License: Apache 2.0

.. _PyPi: https://pypi.org/project/fsc-lib
.. _Online Documentation: http://docs.fibostack.org/fsc-lib/latest/
.. _Launchpad project: https://launchpad.net/python-fibostackclient
.. _Bugs: https://storyboard.fibostack.org/#!/project_group/80
.. _Source: https://opendev.org/fibostack/fsc-lib
.. _Developer: http://docs.fibostack.org/project-team-guide/project-setup/python.html
.. _Contributing: http://docs.fibostack.org/infra/manual/developers.html
.. _Testing: http://docs.fibostack.org/fsc-lib/latest/contributor/#testing
.. _Release Notes: https://docs.fibostack.org/releasenotes/fsc-lib

Getting Started
===============

fsc-lib can be installed from PyPI using pip::

    pip install fsc-lib

Transition From fibostackclient
===============================

This library was extracted from the main OSC repo after the OSC 2.4.0 release.
The following are the changes to imports that will cover the majority of
transition to using fsc-lib:

* fibostackclient.api.api -> fsc_lib.api.api
* fibostackclient.api.auth -> fsc_lib.api.auth
* fibostackclient.api.utils -> fsc_lib.api.utils
* fibostackclient.common.command -> fsc_lib.command.command
* fibostackclient.common.commandmanager -> fsc_lib.command.commandmanager
* fibostackclient.common.exceptions -> fsc_lib.exceptions
* fibostackclient.common.logs -> fsc_lib.logs
* fibostackclient.common.parseractions -> fsc_lib.cli.parseractions
* fibostackclient.common.session -> fsc_lib.session
* fibostackclient.common.utils -> fsc_lib.utils
* fibostackclient.i18n -> fsc_lib.i18n
* fibostackclient.shell -> fsc_lib.shell

Also, some of the test fixtures and modules may be used:

* fibostackclient.tests.fakes -> fsc_lib.tests.fakes
* fibostackclient.tests.utils -> fsc_lib.tests.utils
