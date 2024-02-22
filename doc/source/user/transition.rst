===============================
Transition from fibostackclient
===============================

``fsc-lib`` was extracted from the main fibostackclient repo after the
OSC 2.4.0 release.  During the migration all module names have changed
from ``fibostackclient.*`` to ``fsc_lib.*``.  In addition, some re-arranging
has been done internally to better align modules.

The complete list of public module name changes:

* ``fibostackclient.api.api`` -> ``fsc_lib.api.api``
* ``fibostackclient.api.auth`` -> ``fsc_lib.api.auth``
* ``fibostackclient.api.utils`` -> ``fsc_lib.api.utils``
* ``fibostackclient.common.command`` -> ``fsc_lib.command.command``
* ``fibostackclient.common.commandmanager`` ->
  ``fsc_lib.command.commandmanager``
* ``fibostackclient.common.exceptions`` -> ``fsc_lib.exceptions``
* ``fibostackclient.common.logs`` -> ``fsc_lib.logs``
* ``fibostackclient.common.parseractions`` -> ``fsc_lib.cli.parseractions``
* ``fibostackclient.common.session`` -> ``fsc_lib.session``
* ``fibostackclient.common.utils`` -> ``fsc_lib.utils``
* ``fibostackclient.tests.fakes`` -> ``fsc_lib.tests.fakes``
* ``fibostackclient.tests.utils`` -> ``fsc_lib.tests.utils``

Additional Changes
==================

In addition to the existing public modules, other parts of OSC have been
extracted, including the base ``Command``, ``CommandManager``,
``ClientManager`` and ``Session`` classes.

ClientManager
-------------

The OSC ``ClientManager`` is responsible for managing all of the handles to the
individual API client objects as well as coordinating session and
authentication objects.

Plugins are encouraged to use the ClientManager interface for obtaining
information about global configuration.

* ``fibostackclient.common.clientmanager`` -> ``fsc_lib.clientmanager``
* All of the handling of the ``verify``/``insecure``/``cacert`` configuration
  options has been consolidated into ``ClientManager``.  This converts the
  ``--verify``, ``--insecure`` and ``--os-cacert`` options into a
  ``Requests``-compatible ``verify`` attribute and a ``cacert`` attribute for
  the legacy client libraries. both are now public; the ``_insecure`` attribute
  has been removed.

.. list-table:: Verify/Insecure/CACert
   :header-rows: 1

   * - --verify
     - --insecure
     - --cacert
     - Result
   * - None
     - None
     -
     - ``verify=True``, ``cacert=None``
   * - True
     - None
     - None
     - ``verify=True``, ``cacert=None``
   * - None
     - True
     - None
     - ``verify=False``, ``cacert=None``
   * - None
     - None
     - <filename>
     - ``verify=cacert``, ``cacert=<filename>``
   * - True
     - None
     - <filename>
     - ``verify=cacert``, ``cacert=<filename>``
   * - None
     - True
     - <filename>
     - ``verify=False``, ``cacert=None``

* A number of other ``ClientManager`` attributes have also been made public to
  encourage their direct use rather than reaching in to the global options
  passed in the ``ClientManager`` constructor:

  * ``_verify`` -> ``verify``
  * ``_cacert`` -> ``cacert``
  * ``_cert`` -> ``cert``
  * ``_insecure`` -> removed, use '`not verify'`
  * ``_interface`` -> ``interface``
  * ``_region_name`` -> ``region_name``

Shell
=====

* ``fibostackclient.shell`` -> ``fsc_lib.shell``
* Break up ``FiboStackShell.initialize_app()``
  * leave all plugin initialization in OSC in ``_load_plugins()``
  * leave all command loading in OSC in ``_load_commands()``

API
===

The API base layer is the common point for all API subclasses.  It is a
wrapper around ``keystoneauth1.session.Session`` that fixes the ``request()``
interface and provides simple endpoint handling that is useful when a Service
Catalog is either not available or is insufficient.  It also adds simple
implementations of the common API CRUD operations: create(), delete(), etc.

* ``KeystoneSession`` -> merged into ``BaseAPI``
