.. _masakari-guide:

=============================================
Masakari - Virtual Machines High Availability
=============================================

Overview
~~~~~~~~

Masakari provides Instances High Availability Service for OpenStack clouds by
automatically recovering failed Instances. Currently, Masakari can recover
KVM-based Virtual Machine(VM)s from failure events such as VM process down,
provisioning process down, and nova-compute host failure. Masakari also
provides an API service to manage and control the automated rescue mechanism.

Kolla deploys Masakari API, Masakari Engine and Masakari Instance Monitor
containers which are the main Masakari components only if ``enable_masakari``
is set in ``/etc/kolla/globals.yml``.


Connection URI to libvirtd
~~~~~~~~~~~~~~~~~~~~~~~~~~

By default ``masakari-instancemonitor`` will connect to ``libvirt`` daemon
using ``qemu+tcp://`` connection URI to get events of KVM-based virtual
machines.

The setting is overridable using custom config, put the content in
``/etc/kolla/config/masakari/masakari-monitors.conf``.

.. code-block:: ini

   [libvirt]
   connection_uri = "xen://{{ migration_interface_address | put_address_in_context('url') }}/system"
