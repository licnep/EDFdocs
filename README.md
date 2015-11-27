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

Once you start the virtual machine the files will be available in `/media/sf_share` .

If that doesn't work see the _automount issues_ section

Converting data from xml:
-------------------------

Open a terminal using `ctrl+alt+T`. Run the command `xml2json.py source.xml` where source.xml is your xml file. This will create a folder named `output` that you can later import into anseri.

Converting data from various documents (.doc, .pdf..)
-----------------------------------------------------

Open a terminal using `ctrl+alt+T`. Run the command `dir2json.py source` where source is the folder containing your files. The code will scan the folder and all subfolders and do its best to extract plaintext from all files. It will create a folder named `output` that you can later import into anseri.

Importing data into anseri:
---------------------------

Create a new folder where the anseri database will be stored. The folder must contain a `config_template.cfg` file (you can copy the one in `Desktop/test`). 

To import your data run the command: `python ~/Desktop/EDF/run_anseri.py import edf output` 

Replace `edf` with the name you want to give to the database, and output with the path of the `output` folder containing your data, generated with one of the conversion scripts.

Generating topics:
------------------

To generate topics, run the command: `python ~/Desktop/EDF/run_anseri.py topics sent_edf -nf 16 -nd 32 -nt 64 -s -k interesting words`

Options are as follows:

- `sent_edf`: name of the database. Use `edf` to classify entire documents, `sent_edf` to do sentence-level classification (usually better)
- `-nt`: number of topics to generate
- `-nf`: number of features (words) per topic
- `-nd`: number of documents per topic
- `-s` : print output to a file in the `anseri` subfolder
- `-k` : limit analysis to documents containing the following keyword(s)



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
