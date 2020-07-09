The [previous tutorial sections](https://github.com/lucklab/erplab/wiki/ERPLAB-Tutorial#tutorial-table-of-contents) show the process of loading EEG data into an ERPsets, and getting information from an ERPset through plotting and measurement tools.

Here, we look at the ERPLAB tools for combining and modifying ERPsets.

## Combining multiple subjects ERPsets into Grand Averages
So far in this tutorial, we have focused on the data from example subject 1, producing an ERPset saved as `S1_ERP.erp`. When this ERPset is loaded, we see it as the only entry in the `ERPsets` menu in the EEGLAB window. Most studies will require multiple subjects, and averaging together the ERP data from multiple subjects produces a **Grand Average ERP**. The Grand Average tools in ERPLAB take the ERPsets from multiple subjects, and output a new Grand Average ERPset, which can also be plotted and measured.

Making a Grand Average ERPset has several requirements. In particular, each of the contributing ERPsets should have a matching bins and matching epoch time.

First, let's load the data from multiple subjects. From [tutorial section 1](https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset), `S1_ERP.erp` may have been saved to a file. Repeat the [EEG to ERPset process](https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#load-eeg-data-in-to-eeglab) also for subject 2, producing an ERPset `S2_ERP.erp`. The ERPsets can be created by clicking through those steps in the GUI, or by running a ERPset preparation pipeline script. 

In the EEGLAB window, ensure that the `ERPsets` menu lists all the currently loaded ERPsets. Ensure that both `S1_ERP.erp` and `S2_ERP.erp` are there. If not, load them through `ERPLAB -> Load existing ERPsets`.

![2_ERPsets](https://user-images.githubusercontent.com/5137405/87077184-9a5ae900-c1d7-11ea-8ebc-ac0a48db69dd.png)

_EEGLAB window, showing that S1_ERP and S2_ERP are loaded in ERPLAB, and S2_ERP is the currently selected ERPset_

To run the Grand-Averager tool, hit `ERPLAB -> Average across ERPsets (Grand Average)`.

This will open the following window:

![Grand_Avg](https://user-images.githubusercontent.com/5137405/87078942-34239580-c1da-11ea-84af-83a766b82098.png)

_The Grand Averager window_

Note that there are two options for specifying the ERPsets that will go in the this Grand Average -- either from currently-loaded ERPsets in the ERPset menu, or from a list of previously-saved ERPset files. Here, we have S1_ERP and S2_ERP are loaded in ERPLAB, and so use the top `From ERPset in the ERPset menu` option. The `1 2` in the text box here means the 1st and 2nd ERPsets from the ERPset menu will be used.

Hitting `RUN` will start the Grand Averager. You will see a new window, prompting you to name and save this new ERPset:

![GAv_save_new](https://user-images.githubusercontent.com/5137405/87080044-db54fc80-c1db-11ea-99fe-45de6d449651.png)

_Save newly-produced Grand Average ERPset_

This new Grand Average ERPset is now loaded, and you can see it in the ERPset menu:

![3_ERPsets_with_GAvg](https://user-images.githubusercontent.com/5137405/87080294-456da180-c1dc-11ea-863e-e8aa07f85ef6.png)

The ERPLAB plotting tools, like the ERP Viewer, can then be run as normal on this new ERPset:

![GAv_viewer](https://user-images.githubusercontent.com/5137405/87080543-aeedb000-c1dc-11ea-9959-e398f218e1b1.png)


More information can be seen in the [Grand Averager manual page](https://github.com/lucklab/erplab/wiki/Averaging-Across-ERPSETS-(Creating-Grand-Averages)), which can also be found by hitting the `?` button in each GUI.

<br>
 
## Combining bins for diff waves with Bin Ops

ERPLAB can also create new ERP Bins using the information in existing ERPsets. Most commonly, this is used to create **Difference Waves**, the waveform of the difference of two waveforms. For example, with the P300 example experiment, we have a bin for the frequent condition and a bin for the rare condition. We can create a new bin, bin 3, that is the bin 1 minus bin 2, showing the difference between these two conditions averages.

We do this in a flexible way using bin operations syntax. This format allow specification of advanced custom bins.

To specify a new bin 3 in this format:

**b3 = b2 - b1 label Difference Wave rare-minus-frequent**

Note that the name of this bin is written in text, after the keyword `label`. This equation specifies that a new bin 3 should be created, and it should be the value of bin 2, minus the respective values of bin 1.

This equation is entered in the Bin-Ops GUI.

To begin, make a copy of an ERPset. This can be done by selecting `S1_ERP` in ERPsets menu, then hitting `ERPLAB -> Duplicate or rename ERPset`. Let's call this copy ERPsets `S1_ERP_Difference_Wave_test`. With that `S1_ERP_Difference_Wave_test` as the active ERPset, hit `ERPLAB -> ERP Operations -> ERP Bin Operations'.


![Bin_Ops](https://user-images.githubusercontent.com/5137405/87086240-283dd080-c1e6-11ea-9d71-3fc2d264189c.png)


