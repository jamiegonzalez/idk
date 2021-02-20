ERPLAB is a toolbox plugin for analyzing event-related potential data. It works within the EEGLAB Matlab environment.

### Requirements

* Matlab installed
* EEGLAB folder within Matlab folder path ([download EEGLAB here](https://sccn.ucsd.edu/eeglab/download.php))
* You must have read/write access to the folder containing ERPLAB


There are two ways to install ERPLAB.
1. Use the EEGLAB Plugin Manager
2. Manually place the ERPLAB folder in EEGLAB/plugins

## Install Method 1 - EEGLAB Plugin Manager (Matlab R2018a and after)

From EEGLAB v2019.0, the EEGLAB Plugin Manager includes ERPLAB.

First, run Matlab, and confirm that EEGLAB is in the Matlab path.
The command
`which eeglab` 
will reveal the current path to EEGLAB.
If this path is empty, run `addpath('C:\your_eeglab_path_here')`

Start EEGLAB by running the `eeglab` command at the Matlab Command Window.

In the new EEGLAB window, hit **File > Manage EEGLAB extensions**.

In the EEGLAB Plugin Manger, select **ERPLAB** and hit **install/update**



## Install Method 2 - Manually place the ERPLAB folder in EEGLAB/plugins

First, run Matlab, and confirm that EEGLAB is in the Matlab path.
The command
`which eeglab` 
will reveal the current path to EEGLAB.
If this path is empty, run `addpath('C:\your_eeglab_path_here')`

In your file manager, navigate to that EEGLAB path.

Unzip the ERPLAB folder ([download here](https://github.com/lucklab/erplab/releases)) to the /eeglab/plugins folder.

Ensure that the path is formatted correctly, such that something like C:\your_path_here\EEGLAB\plugins\erplabX.X\eegplugin_erplab.m exists. With that folder path, the folder should look something like:
![ERPLAB_install_path](https://user-images.githubusercontent.com/5137405/101206988-c82c4880-3624-11eb-8f24-c2e0affcd1f4.png)


## Confirm ERPLAB is installed correctly
Start EEGLAB by running the `eeglab` command at the Matlab Command Window.

On running EEGLAB, you should see confirmation that ERPLAB is installed in the Matlab Command Window:
`EEGLAB: adding "ERPLAB" v7.0 (see >> help eegplugin_erplab)`

In the new EEGLAB window, you should see a menu entry for ERPLAB.

Note that ERPLAB has a “working memory” file named memoryerp.erpm that it uses to store various settings (e.g., so that it can remember whether you like to plot positive or negative upward). This file is stored in the folder that contains the ERPLAB code, which is itself stored inside the folder that contains the EEGLAB code. You must have permission to write to that folder. This is not a problem on most personal computers, but it can be an issue on computers that are shared by multiple people (especially large-scale servers). If you are having a problem launching ERPLAB because you don’t have write permission, just install EEGLAB and ERPLAB inside a folder that you own rather than installing it in a folder that is used by multiple people.

For information other installation problems, see our [Frequently Asked Questions](https://github.com/lucklab/erplab/wiki/Troubleshooting-and-Frequently-Asked-Questions) page.

