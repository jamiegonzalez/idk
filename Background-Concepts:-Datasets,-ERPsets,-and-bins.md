## Background Concepts: Datasets, ERPsets, and bins
There are a few key concepts you need to understand before we go any further.  EEGLAB stores a set of EEG data in something called a _dataset_.  A dataset typically stores the data from a single subject, either a single block of trials or an entire session.  A dataset is maintained in memory inside EEGLAB, and it can also be saved on disk.  Whenever you run a routine that changes the data in a dataset, a new dataset is created.  You can see the currently available datasets in the **Datasets** menu.  One dataset is currently active, and any routines that you run will typically be applied to the current dataset.  When a new dataset is created, it becomes the current dataset, but you can make a different dataset active by selecting it in the **Datasets** menu.  This provides a very convenient workflow.

ERPLAB defines an analogous structure called an _ERPset_, which stores a set of ERP waveforms.  They can be active inside ERPLAB and/or saved to disk.  The **ERPsets** menu can be used to see which ERPsets are currently loaded into ERPLAB and to change which ERPset is active.

A _bin_ is a set of averaged ERP waveforms, one for each electrode site, which were created by averaging together a specific set of EEG epochs.  A simple oddball experiment, for example, might have one bin for the infrequent targets and another bin for the frequent standards.  However, a sophisticated experiment might have dozens of different bins, with a given bin being something like "Digits preceded by letters followed by a correct response between 200 and 1000 ms, in a condition in which digits are rare and letters are frequent." In many ERP analysis systems, a bin would be equivalent to a single averaged ERP file.  However, this can lead to a huge number of different files for each subject, making it difficult to keep track of everything. In ERPLAB, an ERPset can contain an unlimited number of bins), and each data processing operation is typically applied to all of the bins in the currently active ERPset.  This saves time and reduces errors.

----
<table style="width:100%">
  <tr>
    <td><a href="./Adding-Channel-Locations-to-your-Dataset"> << Adding Channel Locations to your Dataset </a></td>
    <td><a href="./Tutorial"> Tutorial</a></td>
    <td><a href="./Creating-an-EventList">  Creating an Eventlist >>  </a></td>
  </tr>
</table>
