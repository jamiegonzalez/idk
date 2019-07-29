ERPLAB is a toolbox plugin for analyzing event-related potential data. It works within the EEGLAB Matlab environment.

### Requirements

* Matlab installed
* EEGLAB folder within Matlab folder path ([download EEGLAB here](https://sccn.ucsd.edu/eeglab/download.php))


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

Ensure that the path is formatted correctly, such that something like C:\your_path_here\EEGLAB\plugins\erplabX.X\eegplugin_erplab.m exists.



## Confirm ERPLAB is installed correctly
Start EEGLAB by running the `eeglab` command at the Matlab Command Window.

On running EEGLAB, you should see confirmation that ERPLAB is installed in the Matlab Command Window:
`EEGLAB: adding "ERPLAB" v7.0 (see >> help eegplugin_erplab)`

In the new EEGLAB window, you should see a menu entry for ERPLAB.

