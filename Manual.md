<h2 align="center">ERPLAB TOOLBOX Manual </h2>
<h5 align="center">
Version 6.0<br><br>
User's Manual written by Steve Luck, Candace Markley, Javier Lopez-Calderon, Eric Foo, and Jason Arita<br><br>
ERPLAB Toolbox core designed by Javier Lopez-Calderon and Steve Luck<br>
Additional code by Aaron Simmons, Jason Arita, and Guanghui Zhang<br><br>
</h5>

ERPLAB Toolbox is a freely available, open source set of MATLAB routines for analyzing event-related potential (ERP) data.  It uses the freely available, open source EEGLAB toolbox as a front end.  That is, EEGLAB is used to read in EEG data files and perform various operations on the EEG, and ERPLAB contains a set of new functions, which are added as plug-ins into EEGLAB, extending the set of operations that a user can perform within EEGLAB. These plug-ins include additional EEG processing manipulations (e.g., new functions for marking trials with artifacts) along with functions that provide powerful methods for sorting EEG epochs and averaging them together.  Once a set of averages has been created, they are saved in binary files and can be exported into text files (allowing them to be imported into other ERP analysis systems). ERPLAB also contains  routines that operate on the averaged ERP waveforms (e.g., making difference waves, plotting, filtering, measurement, etc.).

This manual provides a detailed overview of each ERPLAB function, along with data types and other useful background information. For an quick overview of how ERPLAB is used for typical ERP processing, see the [ERPLAB Tutorial](https://github.com/lucklab/erplab/wiki/Tutorial). For a detailed overview of both ERPLAB and the principles underlying ERP processing, see Steve Luck's free online book, [Applied ERP Data Analysis](https://doi.org/10.18115/D5QG92 )

If you run into trouble, check out our [Frequently Asked Questions](https://github.com/lucklab/erplab/wiki/Troubleshooting-and-Frequently-Asked-Questions) page.  All documentation is available on our [GitHub Wiki page](https://github.com/lucklab/erplab/wiki).

If you have bug reports, requests for features, questions about using the software, and comments of general interest, please post them to the ERPLAB Email List.  To communicate privately with the developers, send an email to [erplabtoolbox@gmail.com](mailto:erplabtoolbox@gmail.com).

## Table of Contents
---
- [Installation Information](./Installation)
- [Release Notes For This Version](https://github.com/lucklab/erplab/releases/)
- [Learning To Use ERPLAB Toolbox](./Learning-to-Use-ERPLAB-Toolbox)
- [Basic ERPLAB Processing Steps](./Basic-ERPLAB-Processing-Steps)
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
- [Data Quality Metrics](https://github.com/lucklab/erplab/wiki/ERPLAB-Data-Quality-Metrics)
- [Selecting Optimal Filters with ERPLAB Toolbox](https://github.com/lucklab/erplab/wiki/Selecting-Optimal-Filters-with-ERPLAB-Toolbox)
- [Create and Artificial ERP Waveform](https://github.com/lucklab/erplab/wiki/Create-an-Artificial-ERP-Waveform)

Important note: In some cases, errors will occur leading to a message that instructs you to report the error to the EEGLAB developers. If this happens, please report the error to us at erplab@erpinfo.org and not to the EEGLAB developers.