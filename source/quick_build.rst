.. important::

 A working internet connection, several GB of free disk space and several hours are required by the build process

1. Select Architech's virtual machine from the list of virtual machines inside Virtual Box application

.. image:: _static/vdi_machine_listed.png
    :align: center

2. Click on the icon *Start* button in the toolbar and wait until the virtual machine is ready

.. image:: _static/vbStart.png
    :align: center

3. Double click on *Architech SDK* icon you have on the virtual machine desktop.

.. image:: _static/splash0.jpg
    :align: center

4. The first screen gives you two choices: *ArchiTech* and *3rd Party*. Choose *ArchiTech*.

.. image:: _static/splash1.jpg
    :align: center

5. Select @board@ as board you want develop on. 

.. image:: _static/splashscreen_board_selection.jpg
    :align: center

6. A new screen opens up from where you can perform a set of actions. Click on *Run bitbake* to obtain a terminal ready to start to build an image.

.. image:: _static/splash3.jpg
    :align: center

7. Open *local.conf* file:

.. host::

 | gedit conf/local.conf

8. Go to the end of the file and add the following lines:

.. host::

 | EXTRA_IMAGE_FEATURES_append = " tools-debug debug-tweaks"
 | IMAGE_INSTALL_append = " tcf-agent gdbserver"
 | or
 | EXTRA_IMAGE_FEATURES_append = " tools-debug debug-tweaks"
 | IMAGE_FEATURES_append = " eclipse-debug"


This will trigger the installation of a features set onto the final root file system, like *tcf-agent* and *gdbserver*.

9. Save the file and close gedit.

10. Build *@quickstart-image@* image by means of the following command:

.. host::

 | bitbake @quickstart-image@

At the end of the build process, the image will be saved inside directory:

.. host::

 | /home/@user@/architech_sdk/architech/@board-alias@/yocto/build/tmp/deploy/images/@machine-name@

11. Setup *sysroot* directory on your host machine:

.. host::

 | sudo tar @quickstart-image-tar-options@ /home/@user@/architech_sdk/architech/@board-alias@/yocto/build/tmp/deploy/images/@machine-name@/@quickstart-image@-@machine-name@.@quickstart-image-extension@ -C /home/@user@/architech_sdk/architech/@board-alias@/sysroot/

.. note::

 **sudo** password is: "**@user-password@**"
