<h2 align="center">ERPLAB TOOLBOX Manual </h2>
<h5 align="center">
Version 6.0<br><br>
User's Manual written by Steve Luck, Candace Markley, Javier Lopez-Calderon, Eric Foo, and Jason Arita<br><br>
ERPLAB Toolbox core designed by Javier Lopez-Calderon and Steve Luck<br><br>
</h5>

ERPLAB has primarily been tested using EEG collected with Brain Products ActiCHamp and Biosemi ActiveTwo systems, along with a smaller amount of testing using EEG collected with Neuroscan and EGI systems. Consequently, you should be particularly careful when using this version of ERPLAB with data collected with systems other than Brain Products ActiCHamp or Biosemi ActiveTwo.


## Table of Contents
---
- [Installation Information](./Installation)
- [Release Notes For This Version](https://github.com/lucklab/erplab/releases/)
- [Learning To Use ERPLAB Toolbox](./Learning-to-Use-ERPLAB-Toolbox)
- [Basic ERPLAb Processing Steps](./Basic-ERPLAB-Processing-Steps)
- [Important Background Concepts and Data Structures](./Important-Background-Concepts-and-Data-Structures)
- [Using EEGLAB](./Using-EEGLAB)
- [Preprocessing Continuous EEG](./Preprocessing-Continuous-EEG-Data)
- [The EventList Structure](./The-EVENTLIST-Structure)
- [Creating an EventList](./Creating-An-EVENTLIST)
- [Exporting, Editing, and Importing EventLists](./Exporting,-Editing,-and-Importing-EVENTLISTS)
- [Boundary Events and Disabled Events](./Boundary-Events-and-Disabled-Events)
- [Assigning Events to Bins with BINLISTER](./Assigning-Events-to-Bins-with-BINLISTER)
- [Epoching Bins](./Epoching-Bins)
- [Artifact Detection in Epoched Data](./Artifact-Detection-in-Epoched-Data)
- [Artifact Rejection in Continuous Data](./Artifact-Rejection-in-Continuous-Data)
- [Behavioral Analyses](./Behavioral-Analyses)
- [Computing Averaged ERPs](./Computing-Averaged-ERPs)
- [Getting Information About an ERP from the Matlab Command line](./Getting-Information-about-an-ERP-from-the-Matlab-Command-Line)
- [ERP Bin Operations](./ERP-Bin-Operations)
- [EEG and ERP Channel Operations](./EEG-and-ERP-Channel-Operations)
- [Filtering](./Filtering)
- [Plotting ERP Waveforms](./Plotting-ERP-Waveforms)
- [Topographic Mapping](./Topographic-Mapping)
- [Saving, Loading, Duplicating, Renaming, Clearing, and Exporting Erpsets](./Saving,-Loading,-Duplicating,-Renaming,-Clearing,-and-Exporting-ERPSETS)
- [Appending Erpsets](./Appending-ERPSETS)
- [Averaging Across Erpsets (Creating Grand Averages)](./Averaging-Across-ERPSETS-(Creating-Grand-Averages))
- [ERP Measurement Tool](./ERP-Measurement-Tool)
- [Timing Details](./Timing-Details)
- [Current Source Density (CSD) Tool](./Current-Source-Density-(CSD)-tool)

Important note: The ERPLAB Discussion Forums have been retired. All comments and questions should be posted to the ERPLAB Email List.

Important note: In some cases, errors will occur leading to a message that instructs you to report the error to the EEGLAB developers.  If this happens, please report the error to us at erplab@erpinfo.org and not to the EEGLAB developers.

The purpose of this User's Manual is to provide a detailed description of the ERPLAB functions, along with a discussion of the overall design of the toolbox.  For "how-to" information, see the ERPLAB Tutorial, which provides step-by-step instructions for analyzing a typical set of data.  A [Frequently Asked Questions](./Troubleshooting-and-Frequently-Asked-Questions) document is also available.

If you have bug reports, requests for features, questions about using the software, and comments of general interest, please post them to the ERPLAB Email List.  To communicate privately with the developers, send an email to erplabtoolbox@gmail.com.

ERPLAB Toolbox is a freely available, open source set of MATLAB routines for analyzing event-related potential (ERP) data.  It uses the freely available, open source EEGLAB toolbox as a front end.  That is, EEGLAB is used to read in EEG data files and perform various operations on the EEG, and ERPLAB contains a set of new functions, which are added as plug-ins into EEGLAB, extending the set of operations that a user can perform within EEGLAB. These plug-ins include additional EEG processing manipulations (e.g., new functions for marking trials with artifacts) along with functions that provide powerful methods for sorting EEG epochs and averaging them together.  Once a set of averages has been created, they are saved in binary files and can be exported into text files (allowing them to be imported into other ERP analysis systems).

ERPLAB also contains a set of routines that operate on the averaged ERP waveforms (e.g., making difference waves, plotting, filtering, measurement, etc.).

As in EEGLAB, the ERPLAB routines can be accessed from the Matlab command window and from Matlab scripts in addition to being accessed from the EEGLAB GUI. Consequently, ERPLAB provides the ease of learning of a GUI-based system but also provides the power and flexibility of a scripted system.