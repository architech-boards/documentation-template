Installation
============

Architech's Yocto based SDK is built on top of **@ubuntu-version@**, hence all the scripts
provided are proven to work on such a system.


If you wish to use another distribution/version you might need to change some script
option and/or modify the scripts yourself, remember that you won't get any support in
doing so.

Install a clone of the virtual machine inside your native machine
-----------------------------------------------------------------

To install the same tools you get inside the virtual machine on your native machine
you need to download and run a system wide installation script:

.. host::

 | git clone -b @yocto-version@ https://github.com/architech-boards/machine_installer.git
 | cd machine_installer
 | ./machine_install -g -p

where *-g* option asks the script to install and configure a few graphic customization,
while *-p* option asks the script to install the required packages on the machine.
If you want to install the toolchain on a machine not equal to @ubuntu-version@ then
you may want to read the script, install the required packages by hand, and run it without
options. You might need to recompile the Qt application used to render the splashscreen.

At the end of the installation process, you will get the same tools installed within 
the virtual machine, that is, all the tools necessary to work with Architech's boards.

Install just one board
----------------------

If you don't want to install the tools for all the boards, you can install just the subset
of tools related to @board@:

1) Install repo tool, if you already have it go to step 4

.. host::

 | mkdir -p ~/bin
 | sudo apt-get update
 | sudo apt-get install curl
 | curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
 | chmod a+x ~/bin/repo

2) Make sure directory *~/bin* is included in your *PATH* variable by printing its content

.. host::

 | echo $PATH

3) If *~/bin* directory is not included, add this line to your *~/.bashrc*

.. host::

 | export PATH="$PATH:${HOME}/bin"

4) Install and setup git:

.. host::

  | sudo apt-get install git-core
  | git config --global user.name "Architech User"
  | git config --global user.email ""
  | git config --global color.ui "auto"

5) Finally install the board sdk:

.. host::

 | mkdir @board@
 | cd @board@
 | git clone -b @yocto-version@ https://github.com/architech-boards/@board-splashscreen@.git
 | mv @board-splashscreen@ splashscreen
 | cd splashscreen
 | ./run_install

This script needs the same tools/packages required by *machine_install*
