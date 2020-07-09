The [previous tutorial sections](https://github.com/lucklab/erplab/wiki/ERPLAB-Tutorial#tutorial-table-of-contents) show the process of loading EEG data into an ERPsets, and getting information from an ERPset through plotting and measurement tools.

Here, we look at the ERPLAB tools for combining and modifying ERPsets.

## Combining multiple subjects ERPsets into Grand Averages
So far in this tutorial, we have focused on the data from example subject 1, producing an ERPset saved as `S1_ERP.erp`. When this ERPset is loaded, we see it as the only entry in the `ERPsets` menu in the EEGLAB window. Most studies will require multiple subjects, and averaging together the ERP data from multiple subjects produces a **Grand Average ERP**. The Grand Average tools in ERPLAB take the ERPsets from multiple subjects, and output a new Grand Average ERPset, which can also be plotted and measured.

First, let's load the data from multiple subjects. From [tutorial section 1](https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset), `S1_ERP.erp` may have been saved to a file. Repeat the [EEG to ERPset process](https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#load-eeg-data-in-to-eeglab) also for subject 2, producing an ERPset `S2_ERP.erp`. The ERPsets can be created by clicking through those steps in the GUI, or by running a ERPset preparation pipeline script. 

In the EEGLAB window, ensure that the `ERPsets` menu lists all the currently loaded ERPsets. Ensure that both `S1_ERP.erp` and `S2_ERP.erp` are there. If not, load them through `ERPLAB -> Load existing ERPsets`. 