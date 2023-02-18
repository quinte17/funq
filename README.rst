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

  LD_PRELOAD=PATHTO/libFunq.so ./funq-test-app

Then you can call from python like this::

  from funq.client import FunqClient

  btn = cl.widget(path='mainWindow::QWidget::click')
  btn.click()

  btn = cl.widget(path='mainWindow::ClickDialog::QPushButton')
  btn.click()

  if cl.widget(path='mainWindow::statusBar::QLabel').properties()['text'] == 'clicked !':
      print("we did it!")


Installation
============

This is gonna change.

Funq consists of two parts. libFunq.so is the preloaded library which includes the funq-server the client connects to.
The python package funq is the client which connects to a funq-server.
In big environments it is not always easy to start the gui application and find the proper port. One idea
could be, to patch your local copy of qt to magically load the lib and find an unused port. Then create
a file named with the pid of the process and write the corresponding port into it.
If you have a setup like this you could provide an automagic connect for your tests if you can map the
process name with the corresponding pid and port.

The libFunq.so should not be part of the python package, because there is no guarantee to have python
on the target and you have much more control for the used compiler flags and target architecture.

libFunq: to build the libFunq.so you need cmake::

  mkdir server/libFunq/build
  cd server/libFunq/build
  cmake ../
  make

python funq client::

  cp -ar client/funq PATHON/site-packages

or maybe it is possible to provide some pip package in the future. Or if you have artifactory you could provide
yourself the python package.

tests: to build the helper programm::

  mkdir tests-functionnal/funq-test-app/build
  cd tests-functionnal/funq-test-app/build
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
