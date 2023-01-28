The *funq* project
==================

**WORK IN PROGRESS**

**funq** is a tool to write FUNctional tests for Qt applications, both Widgets
and QML, using python.

It is licenced under the CeCILL v2.1 licence (very close to the GPL v2).
See the LICENCE.txt file distributed in the sources for more information.

The licence may appear restrictive, but as **funq** is a testing tool, you
probably just don't mind. Do not deliver funq alongside your code source
or compiled binaries if your licence is not compatible, that's all. You can
still use the sources, or link with funq libraries for a personal use
(like testing!).

Please feel free to contribute to this project by creating github issues,
pull requests, or simply staring the project! It will be greatly appreciated.

Examples
========

Run your application like::

  funq --host 0.0.0.0 --port 9000 YourApp

Then you can call from python like this::

  from funq.client import FunqClient

  funq = FunqClient("192.168.0.17", 9000)
  funq.widget('btnTest').click()


Installation
============

This is gonna change.

libFunq: to build the libFunq.so you need cmake::

  mkdir server/libFunq/build
  cd server/libFunq/build
  cmake ../
  make

How does *funq* works
=====================

**funq** is divided in two parts:

- **funq-server** is the server part of the project, composed of an
  executable called **funq** and a dynamic library **libFunq**. The
  **funq** executable allows to inject some code in a Qt application
  to start a TCP server that will allow to interact with the application.
  This is currently not working with Python 3 on Windows, but you can still
  build you application with libFunq as a workaround.

- **funq** is a python package that offers an API to interact with a
  **libFunq** TCP server. It is the client side of the project, and uses
  nosetests to launch FUNctional Qt tests.

Known restrictions
==================

Main focus is Linux atm.

Documentation
=============
Documentation is available at https://funq.readthedocs.io/

Thanks to
=========

Thanks to Yann De Poulpiquet <yann_de_poulpiquet@bestmail.us> and
Riad Lezzar <rlezzar@gmail.com> to have contributed by writing the firsts
functional tests with **funq**.

Thanks also to Jean-Luc Rouzoul, Dominique Constant and Mickaël Guérin for
having supported this project.

Without them, **funq** would never have become a free software !
