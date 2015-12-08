## Installation Information
To see a list of new and updated features for this version, see the Release Notes.

A video demonstrating the installation process for ERPLAB 2.0 is available (click here to access). The installation procedure is nearly identical for version 4.0.

## Requirements
- Matlab versions 2010a, 2012a, 2014b, 2015
  - **Matlab's Signal Processing Toolbox is required.**

- [EEGLAB Toolbox](http://sccn.ucsd.edu/eeglab/) version 9, 12, 13 
  - **Do not use version 11 of EEGLAB**

- Operating System
  - ERPLAB has mainly been tested with Mac OS X and Windows.  
  - It should work with Linux, but this has not been extensively tested.
  - EEGLAB and ERPLAB work best if you have plenty of RAM. We recommend at least 8 GB. Note, however, that your computer will not be able to take advantage of more than 4 GB of RAM unless you have a 64-bit version of Matlab installed (along with a 64-bit operating system).

## Basic Steps
ERPLAB can be downloaded here.

To install ERPLAB:

1. Make sure that EEGLAB is not running
2. Place the ERPLAB folder inside the EEGLAB plugins folder. For example, you might place ERPLAB in a path like this:
`Documents > MATLAB > eeglab12_0_1_0b > plugins`

> Note: Due to differences among operating systems, the ERPLAB files are sometimes embedded within an additional folder layer. You should make sure that the erplab folder inside the EEGLAB plugins folder contains a file named eegplugin_erplab.m. If it does not, but instead contains another folder with "erplab" in the name, you may need to eliminate the enclosing erplab folder.

Matlab keeps information about where programs and other files are located in a path variable.  When you first put ERPLAB into the EEGLAB plugins folder, Matlab doesn't know to look in this folder.  Recent versions of EEGLAB (version 12 and higher) will automatically look in the plugins folder and add any plugins to the path (including the ERPLAB plugin).  If you are using an older version of EEGLAB, you will need to manually add the ERPLAB folder to the path. To accomplish this, launch MATLAB and choose File > Set Path. If you are upgrading from a previous installation, you should remove any elements of the the path from the previous installation (anything with "erplab" in it). Then select Add with subfolders.  Browse to select the path for the erplab folder in the EEGLAB plugins folder, which will look something like this: `Documents > MATLAB >  eeglab12_0_1_0b > plugins > erplab_4.0.0.137`


Then save your new path. With older versions of EEGLAB, you must update the path every time you install a new version of ERPLAB.

----
### Verifying that ERPLAB has been properly installed
To verify that ERPLAB has been installed, launch EEGLAB (and the included ERPLAB plug-in) by typing eeglab in the MATLAB command window.  You can verify that ERPLAB is installed by looking for the ERPLAB menu in the EEGLAB GUI, as shown in the screenshot below:

![ERPLAB Menu](https://github.com/lucklab/erplab/wiki/images/manual-installation-erplab_menu.jpg)

 

----
### Hints and Troubleshooting
Most installation problems arise from not including all of the ERPLAB folders in the Matlab path.  If you get error messages when using nearly every command in the ERPLAB menu, this is probably a path problem.  Path problems also typically lead to error messages like this: Undefined function or method 'gui_mainfcn' for input arguments of type 'struct'.  If you have either of these problems, you should check to see whether your path includes ERPLAB by typing path in the Matlab command window.  This will list all folders in your path.  You should see several lines in your path that contain "plugins/erplab_4.0".  If you don't, you should try updating your path again.  Make sure that you click Add with subfolders when you add the path.  And make sure that you save your new path before closing the window that you used to set your path.

If you see a large number of warning messages when you launch EEGLAB, you may need to remove the folders with 'external/fieldtrip' in the Matlab Path.

If you install a new version of EEGLAB, you can simply move the ERPLAB folder from the plugins folder of the old version of EEGLAB to the new version (and then update the path). 

You must delete any previous version of ERPLAB before installing the new version.  A convenient way to do this and retain the old version is to convert the old version into a compressed archive (e.g., a .zip or .sit file).  If you simply move the old folder, it may still be accessed by Matlab (depending on how your computer's operating system handles paths), and this could cause problems.  So we strongly recommend that you either delete the old folder or convert it to a compressed archive.

If you run into bugs, you may want to quit from EEGLAB, type 'clear all', and re-launch EEGLAB.  You may even want to quit and restart Matlab.

In EEGLAB, we recommend that you go to EEGLAB > File > Memory and other options and make sure that "If set, when browsing to open a new dataset assume the folder/directory of previous dataset" is NOT checked.  Otherwise EEGLAB will sometimes ignore Matlab's current directory when looking for files.

----
### Windows Installation Issues
When extracting ERPLAB into the same folder as the ERPLAB ZIP-file, Windows creates a nested folder that envelopes that actual ERPLAB folder containing the functions and sub-folders. This nested folder prevents EEGLAB from recognizing that ERPLAB is correctly installed. 

##### Two ways to install ERPLAB in Windows:

Double-click the ERPLAB zip-file. This opens a new window containing the ERPLAB folder. Drag-and-drop the ERPLAB folder to the EEGLAB plugins folder to install ERPLAB.
Right-click on the folder and then select "Extract all...". When specifying the destination folder to extract to, browse to the EEGLAB plugins folder. Complete the rest of the extraction steps. Windows will correctly create the ERPLAB folder in the EEGLAB plugins folder without the nesting.