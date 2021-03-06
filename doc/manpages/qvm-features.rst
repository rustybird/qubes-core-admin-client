.. program:: qvm-features

:program:`qvm-features` -- manage domain's features
===================================================

Synopsis
--------

:command:`qvm-features` [-h] [--verbose] [--quiet] *VMNAME* [*FEATURE* [*VALUE*]]

Options
-------

.. option:: --help, -h

   show this help message and exit

.. option:: --verbose, -v

   increase verbosity

.. option:: --quiet, -q

   decrease verbosity

.. option:: --unset, --default, --delete, -D

   Unset the feature.

Description
-----------

This command is used to manually manage the *features* of the domain. The
features are key-value pairs with both key and value being strings. They are
used by extensions to store information about the domain and make policy
decisions based on them. For example, they may indicate that some specific
software package was installed inside the template and the domains based on it
have some specific capability.

.. warning::

   The features are normally managed by the extensions themselves and you should
   not change them directly. Strange things might happen otherwise.

Some extensions interpret the values as boolean. In this case, the empty string
means :py:obj:`False` and non-empty string (commonly ``'1'``) means
:py:obj:`True`. An absence of the feature means "default", which is
extension-dependent. In most cases the default value for feature is retrieved
from a qube template.

List of known features
----------------------

.. warning::

   This list of features may be incomplete, because extensions are free to use any
   values, without registering them anywhere.

gui
^^^

Qube provide any kind of GUI. Setting this feature to :py:obj:`False` disable
GUI for given qubes - both gui-agent based and emulated VGA based one. Setting
this feature to :py:obj:`True` enable gui-agent based GUI (i.e. with support of
tools installed inside of qube). Not setting this feature at all, enable showing
VGA emulated output.

Default: show emulated VGA output only

qrexec
^^^^^^

Qube has qrexec agent installed - i.e. it is possible to request staring a
command/service in there.

Default: assume qrexec not installed (do not wait for it while starting the
qube)

rpc-clipboard
^^^^^^^^^^^^^

Use `qubes.ClipboardCopy` and `qubes.ClipboardPaste` qubes RPC services to
fetch/send clipboard content from/to this qube, instead of using GUI protocol.
This is supported (and required) by Qubes Windows Tools.

Default: use GUI protocol for clipboard operations

no-monitor-layout
^^^^^^^^^^^^^^^^^

When set to :py:pbj:`True`, monitor layout is not sent to this qube. That is
avoid calling `qubes.SetMonitorLayout` in this qube.

Default: send monitor layout

internal
^^^^^^^^

Internal qubes (with this feature set to :py:obj:`True`) are not included in the
menu.

Default: not internal VM

appmenus-legacy
^^^^^^^^^^^^^^^

Generate legacy menu entries, using `qubes-desktop-run` command inside a VM,
instead of `qubes.StartApp` qrexec service. This is used for qubes imported from
previous Qubes version.

Default: new style menu entries, using `qubes.StartApp` service

appmenus-dispvm
^^^^^^^^^^^^^^^

Generate menu entries for starting applications in Disposable VM based on given
AppVM, instead of this AppVM directly.

Default: create menu entries for AppVM itself

qubes-firewall
^^^^^^^^^^^^^^

Setting this to :py:obj:`True` means that qube support enforcing firewall rules
set with `qvm-firewall` command.

Default: assume qubes-firewall not enforced

net.fake-ip
^^^^^^^^^^^

Hide the real IP of the qube from it, and configure it with value set to this
feature. Note that you can assign the same `net.fake-ip` address to multiple
qubes and it shouldn't cause any troubles (unless you want to two such qubes
communicate with each other). This feature does not affect address used in
firewall rules, routing tables etc.

Default: do not hide IP (qube's `ip` property) from the qube

net.fake-gateway
^^^^^^^^^^^^^^^^

Hide the real gateway of the qube from it, and configure it with value set to
this feature.

Default: do not hide geteway (qube's `gateway` property) from the qube

net.fake-netmask
^^^^^^^^^^^^^^^^

Hide the real netmask of the qube from it, and configure it with value set to
this feature.

Default: do not hide netmask (qube's `netmask` property) from the qube

updates-available
^^^^^^^^^^^^^^^^^

There are updates available. In most cases it is useful to (only) read this
feature to check if qube needs to be updated.

Default/no value: no updates available

video-model
^^^^^^^^^^^

Choose video card modes emulated by QEMU for this qube. For available values see
libvirt documentation about <video><model type=...> element:
https://libvirt.org/formatdomain.html#elementsVideo
Some systems (Windows) works better with 'cirrus' model set here.

Default: vga

Authors
-------

| Joanna Rutkowska <joanna at invisiblethingslab dot com>
| Marek Marczykowski <marmarek at invisiblethingslab dot com>
| Wojtek Porczyk <woju at invisiblethingslab dot com>

.. vim: ts=3 sw=3 et tw=80
