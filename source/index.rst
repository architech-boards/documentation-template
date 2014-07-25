************@board-size:*@**************
Architech's @board@ documentation
************@board-size:*@**************

.. image:: _static/board.png
    :align: center

.. only:: html

.. include:: index_custom.rst

If you are a new user of the **Yocto based SDK** we suggest you to read the :ref:`quick` chapter,
otherwise, if you want to have a better understanding of specific topics, just jump directly to
the chapter that interests you the most.

Furthermore, we encourage you to read the `official Yocto Project documentation <https://www.yoctoproject.org/documentation>`_.

Notations
=========

Throughout this guide, there are commands, file system paths, etc., that can either refer to the
machine (real or virtual) you use to run the SDK or to the board.

.. host::

 This box will be used to refer to the machine running the SDK

.. board::

 This box will be used to refer to @board@ board

However, the previous notations can make you struggle with long lines. In such a case, the following
notation is used.
 
.. host::

 | This Box will be used where long lines need to be displayed, as well as with system paths, commands, configuration files, etc.
 | All related to the host.
 | It will be used to display code example as well.

.. board::

 | The same facility will be used, when needed, for the board.

If you click on *select* on the top right corner of these two last boxes, you will get the text inside the box selected.
We have to warn you that your browser might select the line numbers as well, so, the first time you use such a feature,
you are invited to check it.

Sometimes, when referring to file system paths, the path starts with **/path/to**. In such a case, the documentation is **NOT**
referring to a physical file system path, it just means you need to read the path, understand what it means, and understand
what is the proper path on your system. For example, when referring to the device file associated to your USB flash memory you
could read something like this in the documentation:

.. host::

 | /path/to/your/USB/device

Since things are different from one machine to another, you need to understand its meaning and corresponding value for your
machine, like for example:

.. host::

 | /dev/sdb

Chapters
========

.. toctree::
  :maxdepth: 2
  :numbered:

  @unboxing@
  quick
  sdk-architecture
  create-sdk
  bsp
  tools
  board
  @add-ons@
  faq
