Test running
============

Virtual testing
---------------

If you are on a non-Linux system install VirtualBox_ and Vagrant_, and run
``make vagrant-test``.

You may specify arbitrary :program:`py.test` arguments by ``TESTARGS``::

   make TESTARGS='--enable-privileged -k observer --verbose' vagrant-test

Vagrant automatically fetches, installs and provisions a virtual machine based
on Ubuntu Lucid.  This virtual machine has the pyudev source code linked in as
shared folder under ``/vagrant``, and two virtualenvs for Python 2 and Python 3
with all dependencies installed at ``~/pyudev-py2`` and ``~/pyudev-py3``
respectively.  Use ``vagrant ssh`` to get a shell on this machine.


Direct testing using tox_
-------------------------

If you are on a Linux system run all tests with tox_.  This tool automatically
creates virtualenvs (see virtualenv_), installs all packages required by the
test suite, and runs the tests.

Run all pyudev tests against Python 2.7, Python 3.2 and PyPy::

   tox -e py27,py32,pypy

Pass any arguments you want to :program:`py.test` after two dashes ``--``::

   tox -e py27,py32,pypy -- --enable-privileged


Notes
-----

Device samples
~~~~~~~~~~~~~~

Many pyudev tests run against the real device database of the system the tests
are executed on.  As testing against the whole database takes a long time,
tests are run against a random sample by default.  With the command line
options provided by :mod:`~tests.plugins.udev_database` you can configure the
size of this sample, or run the tests against a single device or the whole
database.


Privileged tests
~~~~~~~~~~~~~~~~

Some tests need to execute privileged operations like loading or unloading of
kernel modules to trigger real udev events.  These tests are disabled by
default.  Refer to :mod:`~tests.plugins.privileged` for more information on how
to enable these tests and configure them properly.

.. _virtualbox: https://www.virtualbox.org/
.. _vagrant: http://vagrantup.com/
.. _virtualenv: http://www.virtualenv.org/en/latest/index.html
.. _tox: http://tox.testrun.org/latest/
