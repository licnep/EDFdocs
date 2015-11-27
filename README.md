Setup:
======

Open Virtual Box (if you don't have it download it [here](https://www.virtualbox.org/wiki/Downloads)). 
and create a new virtual machine using the provided vdi image (the password is `sumup`).

Sharing a folder for analysis
-----------------------------

This should be done with the virtual machine turned off, otherwise the settings will not be permanent. Open the VM Settings and go to Shared Folders.

![Step 1](img/step1.png)

![Step 2](img/step2.png)

Click on the button to add a shared folder.

![Step 3](img/step3.png)
 
Choose the folder you want to work on. Name the shared folder "share", and activate automount.

![Step 4](img/step4.png)

Once you start the virtual machine the files will be available in the `share` folder on the desktop.

If that doesn't work see the _automount issues_ section


Usage:
======

On the desktop you will find a folder named `share`, if the setup worked the folder should contain your files.

Open a terminal using `ctrl+alt+T`.

Run the command: `dir2json.py ~/Desktop/share/`

(Replace `~/Desktop/share/` with another folder if needed)

If everything worked correctly this should create a file named `output.json` in your current directory (usually the home directory), which can then be passed to Anser Indicus for analysis.


Common issues:
==============

Keyboard Layout
---------------

If you are unable to enter certain characters you may need to change the keyboard layout in the top right corner:

![Layout](img/layout.png)


Automount issues
----------------

If the shared folder doesn't mount automatically open a terminal (`Ctrl+alt+T`) and run:

`sudo mount -t vboxsf -o rw,uid=1000,gid=1000 share ~/Desktop/share`

(Replace `~/Desktop/share/` with another folder if needed)

Shared folder permissions
-------------------------

If you can't access the shared folder you probably need to add your user to the vboxsf group:

`sudo adduser <user> vboxsf`


"Cannot register the hard disk"
-------------------------------

This happens when a virtual machine is already using a .vdi image with the same UUID. To change the image UUID run:

`VBoxManage internalcommands sethduuid disk.vdi`

Where disk.vdi is the name of the vdi you want to use.

For any other issue, contact alessandro.preziosi@sumupanalytics.com
