Yocto
=====

If you have launched machine_installer or run_install.sh script, yocto is already installed. 
The following steps are useful for understood how the sdk works "under the hood".

Installation with repo
----------------------

The easiest way to setup and keep all the necessary meta-layers in sync with upstream repositories
is achieved by means of Google's **repo** tool.
The following steps are necessary for a clean installation:

1) Install repo tool, if you already have it go to step 4

.. host::

 | mkdir -p ~/bin
 | sudo apt-get install curl
 | curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
 | chmod a+x ~/bin/repo

2) Make sure directory *~/bin* is included in your *PATH* variable by printing its content

.. host::

 | echo $PATH

3) If *~/bin* directory is not included, add this line to your *~/.bashrc*

.. host::

 | export PATH="$PATH:${HOME}/bin"

4) Open a new terminal

5) Change the current directory to the directory where you want all the meta-layers to be downloaded into

6) Download the manifest

.. host::

 | repo init -u https://github.com/architech-boards/@manifest-repository@.git -b @yocto-version@ -m manifest.xml

7) Download the repositories

.. host::

 | repo sync

By the end of the last step, all the necessary meta-layers should be in place, anyway, you still need to 
edit your **local.conf** and **bblayers.conf** to compile for @machine-name@ machine and using all the downloaded
meta-layers.

Updating with repo
------------------

When you want your local repositories to be updated, just:

1) Open a terminal

2) Change the current directory to the directory where you ran repo init

3) Sync your repositories with upstream

.. host::

 | repo sync

Install Yocto by yourself
-------------------------

If you really want to download everything by hand, just clone branch *@yocto-version@* of *@meta-layer@*:

.. host::

 | git clone -b @yocto-version@ @meta-layer-remote@/@meta-layer@.git

and have a look at the README file.

To install *Eclipse*, *Qt Creator*, *cross-toolchain*, *NFS*, *TFTP*, etc., read **Yocto**/**OpenEmbedded** documentation, along
with the other tools one.
