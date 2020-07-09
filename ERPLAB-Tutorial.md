<h2 align="center">ERPLAB TOOLBOX TUTORIAL </h2>
<h5 align="center">
Version 8.0 tutorial written by Andrew X Stewart <br><br>
ERPLAB Toolbox team -  Andrew X Stewart, Javier Lopez-Calderon and Steve Luck<br><br>
</h5>


ERPLAB is a toolbox to create, process, view, and measure ERPs (Event Related Potentials) from EEG data. It uses the Matlab programming environment and some functions from the EEGLAB toolbox.

In this tutorial, we provide step-by-step instructions for processing a simple data set. The goal will be to view and measure ERPs from each subject, from the provided simple EEG datasets.

More documentation is provided for specific functions in the [ERPLAB User Manual](https://github.com/lucklab/erplab/wiki/Manual), which can also be accessed from the '?' links within the ERPLAB GUI.

# Tutorial Table of Contents

### [Overview and ERPsets](https://github.com/lucklab/erplab/wiki/ERPLAB-Tutorial#tutorial-table-of-contents) <br><br>

### [**Part 1 - EEG to ERPset**](https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset) <br>
  * [Getting Started, Loading an EEG dataset](https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset) <br>
  * [Attaching an EventList](https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#events-and-the-eventlist) <br>
  * [Assigning trials to bins](https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#assigning-trials-to-bins) <br>
  * [Extract bin-based EEG Epochs](https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#extract-bin-based-epochs) <br>
  * [Artifact detection](https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#artifact-detection) <br>
  * [Creating Averaged ERPs](https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#create-averaged-ERPs) <br> <br>

### [**Part 2 - ERP Plotting and Measuring**](https://github.com/lucklab/erplab/wiki/Tutorial-2-ERP-Plotting-and-Measuring) <br>
* [ERP Viewer tool](https://github.com/lucklab/erplab/wiki/Tutorial-2-ERP-Plotting-and-Measuring#erp-viewer)
* [Plotting ERPs](https://github.com/lucklab/erplab/wiki/Tutorial-2-ERP-Plotting-and-Measuring#plot-erp-waveforms)
* [Measuring ERPs](https://github.com/lucklab/erplab/wiki/Tutorial-2-ERP-Plotting-and-Measuring#erp-measurement-tool)
* Viewing data quality measures <br> <br>

### [**Part 3 - Combining and modifying ERPsets**](https://github.com/lucklab/erplab/wiki/Tutorial-3-Combining-and-Modifying-ERPsets) <br>
*  [Combining subjects in to Grand Averages](https://github.com/lucklab/erplab/wiki/Tutorial-3-Combining-and-Modifying-ERPsets#combining-multiple-subjects-erpsets-into-grand-averages) <br>
*  [Combining bins for diff waves with Bin Ops](https://github.com/lucklab/erplab/wiki/Tutorial-3-Combining-and-Modifying-ERPsets#combining-bins-for-diff-waves-with-bin-ops) <br>
*  Combining channels with Chan Ops, channel labels <br>
*  Filtering, on EEG sets and ERP sets <br>
*  Typical pipelines, order-of-processing, and scripting <br>
<br> <br>

## Using ERPLAB - Overview

The EEG data saved from a subject in an experiment is typically 'continuous EEG' - that is, EEG data that is arranged in a format of (number of electrodes) * (number of time-points). When running ERP experiment, we often wish to compare the event-related potential in response to one event compared to another - perhaps rarely-shown stimulus compared to frequently-shown stimulus for a P300 experiment. To get from continuous EEG to plotting and measuring ERPs, several steps are necessary:

#### Attach an EventList
We need to know when the events occurred within the time course of the EEG data. For this we construct an EventList structure. This has a list of what events occurred when, and in a way that we can edit, and group events in to *Bins*.

#### Assign Events to Bins
For your analysis, different sets of trials/events may need be grouped together for different comparisons. In this tutorial example experiment, we want to group together trials with frequent stimuli (indicated with event codes of {11,122,22,111}) and also group together trials that had rare stimuli (indicated with event codes of {21,112,12,121}).

ERPLAB has flexible tools for assigning event to bins, including Binlister which allows detailed specification of bin event criteria.


#### Continuous EEG -> Bin-Based-Epoched EEG

With an Eventlist and bin-criteria, the continuous EEG can be extracted to bin-based epochs. Epochs are short stretches of EEG data, perhaps 1 second long. Epochs will be anchored around specific event markers, with some time before and after. Rather than the previous continuous EEG data stored in the format of

` (number of electrodes) * (number of time-points) `

epoched EEG data will now be stored in the format of 

`(number of electrodes) * (number of time-points in epoch) * (number of epochs/trials) `


#### Creating Averaged ERP Sets

From this bin-epoched EEG set, we create a new structure that explicitly has the averaged ERP. Averaging each bin in the above bin-epoched EEG data give us ERP data in the format:

` (number of electrodes) * (number of time-points in epoch) * (number of bins) `

With the data prepared in this ERP set, we can access and plot the data from each condition:

![ERP_Viewer2](https://user-images.githubusercontent.com/5137405/82585605-1b3c2380-9b4b-11ea-938a-91def4b6684d.png)



<!--Bottom Navigation HTML-->
<br><br><br><br>
----
<table >
  <tr>
    <td  align="right" width="40%">
    </td>
    <td  align="center" width="20%">
      <a href="https://github.com/lucklab/erplab/wiki/ERPLAB-Tutorial#tutorial-table-of-contents">
        <img src="https://github.com/lucklab/erplab/wiki/images/ionicicons/ios7-copy.png" alt="tutorial icon" height="75">
        <br>
        Tutorial list
       </a>
    </td>
    <td  align="left" width="40%">
      <a href=https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset>
        <img src="https://github.com/lucklab/erplab/wiki/images/ionicicons/ios7-arrow-forward.png" alt="forward arrow" height="75">
        <br>
        Getting Started, loading EEG data
      </a>
    </td>
  </tr>
</table>