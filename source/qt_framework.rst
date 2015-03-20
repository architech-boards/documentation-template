.. _qt_framework_label:

Qt Framework
============

The Qt Framework used by this SDK is composed of libraries for your host machine and your target.
To compile the libraries for *x86* you only need your distribution toolchain, while to compile the
libraries for @board@ board you need the proper cross-toolchain (see Chapter :ref:`manual_compilation_label`
for further information on how to get it).

This section just wants to show you how the framework has been generated.

Before to begin, keep in mind you might need to install the following package to compile yourself
the libraries under Ubuntu

.. host::

 | sudo apt-get install libxrender-dev

So, to install *qt-everywhere* for *x86* from sources, the usual drill of download, uncompress, *configure*,
*make* and *make install* is required:

.. host::

 | wget http://download.qt-project.org/official_releases/qt/4.8/4.8.6/qt-everywhere-opensource-src-4.8.6.tar.gz
 | tar -zxf qt-everywhere-opensource-src-4.8.6.tar.gz
 | cd qt-everywhere-opensource-src-4.8.6
 | ./configure /*Choose Open source Edition when asked, and accept the license*/
 | make
 | make install 

The installation of the libraries for @board@ from sources is sligthly more complicated. Once you downloaded
and uncompressed the sources

.. host::

 | wget http://download.qt-project.org/official_releases/qt/4.8/4.8.6/qt-everywhere-opensource-src-4.8.6.tar.gz
 | tar -zxf qt-everywhere-opensource-src-4.8.6.tar.gz
 | cd qt-everywhere-opensource-src-4.8.6
 | cp -r mkspecs/qws/linux-arm-g++/ mkspecs/qws/linux-@board-alias@-g++
 | cd mkspecs/qws/linux-@board-alias@-g++/
 | gedit qmake.conf

you need to customize *qmake* configuration

.. host::

 | #
 | # qmake configuration for building with arm-linux-g++
 | #
 | 
 | include(../../common/linux.conf)
 | include(../../common/gcc-base-unix.conf)
 | include(../../common/g++-unix.conf)
 | include(../../common/qws.conf)
 | 
 | # modifications to g++.conf
 | QMAKE_CC                = arm-poky-linux-@eabi@-gcc --sysroot=/home/@user@/architech_sdk/architech/@board-alias@/toolchain/sysroots/@arm-toolchain-directory@
 | QMAKE_CXX               = arm-poky-linux-@eabi@-g++ --sysroot=/home/@user@/architech_sdk/architech/@board-alias@/toolchain/sysroots/@arm-toolchain-directory@
 | QMAKE_LINK              = arm-poky-linux-@eabi@-g++ --sysroot=/home/@user@/architech_sdk/architech/@board-alias@/toolchain/sysroots/@arm-toolchain-directory@
 | QMAKE_LINK_SHLIB        = arm-poky-linux-@eabi@-g++ --sysroot=/home/@user@/architech_sdk/architech/@board-alias@/toolchain/sysroots/@arm-toolchain-directory@
 | 
 | # modifications to linux.conf
 | QMAKE_AR                = arm-poky-linux-@eabi@-ar cqs
 | QMAKE_OBJCOPY           = arm-poky-linux-@eabi@-objcopy
 | QMAKE_STRIP             = arm-poky-linux-@eabi@-strip
 | 
 | load(qt_config)

save the file and exit from gedit, then *configure*, *make* and *make install*

.. host::

 | cd ../../../
 | ./configure -no-pch -opensource -confirm-license -prefix /usr/local/Trolltech/@qt-libs-alias@ -no-qt3support -embedded arm -nomake examples -nomake demo -little-endian -xplatform qws/linux-@board-alias@-g++ -qtlibinfix E
 | make
 | make install

A comfortable tool to get your job done with Qt is *Qt Creator*, which its use will be introduced
in Section :ref:`qt_creator_label`. You can download it from here:

.. tip::

 | wget http://sourceforge.net/projects/qtcreator.mirror/files/Qt%20Creator%202.8.1/qt-creator-linux-x86-opensource-2.8.1.run/download
