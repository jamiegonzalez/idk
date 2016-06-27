| ERPLAB TOOLBOX USER'S MANUAL| 
| :----- |
| Version 4.0 |
| 01 October 2013 |


User's Manual written by Steve Luck, Candace Markley, Javier Lopez-Calderon, Eric Foo, and Jason Arita
ERPLAB Toolbox core designed by Javier Lopez-Calderon and Steve Luck



Table of Contents

- [INSTALLATION INFORMATION](https://github.com/lucklab/erplab/wiki/Installation)
- [RELEASE NOTES FOR THIS VERSION](https://github.com/lucklab/erplab/releases/)
- [LEARNING TO USE ERPLAB TOOLBOX](https://github.com/lucklab/erplab/wiki/Learning-to-Use-ERPLAB-Toolbox)
- [BASIC ERPLAB PROCESSING STEPS](https://github.com/lucklab/erplab/wiki/Basic-ERPLAB-Processing-Steps) 
- [IMPORTANT BACKGROUND CONCEPTS AND DATA STRUCTURES](https://github.com/lucklab/erplab/wiki/Important-Background-Concepts-and-Data-Structures)
- [USING EEGLAB](https://github.com/lucklab/erplab/wiki/Using-EEGLAB)
- [THE EVENTLIST STRUCTURE](https://github.com/lucklab/erplab/wiki/The-EVENTLIST-Structure)
- [CREATING AN EVENTLIST](https://github.com/lucklab/erplab/wiki/Creating-An-EVENTLIST)
- [EXPORTING, EDITING, AND IMPORTING EVENTLISTS](https://github.com/lucklab/erplab/wiki/Exporting,-Editing,-and-Importing-EVENTLISTS)
- [BOUNDARY EVENTS AND DISABLED EVENTS](https://github.com/lucklab/erplab/wiki/Boundary-Events-and-Disabled-Events)
- [ASSIGNING EVENTS TO BINS WITH BINLISTER](https://github.com/lucklab/erplab/wiki/Assigning-Events-to-Bins-with-BINLISTER)
- [EPOCHING BINS](https://github.com/lucklab/erplab/wiki/Epoching-Bins)
- [ARTIFACT DETECTION IN EPOCHED DATA](https://github.com/lucklab/erplab/wiki/Artifact-Detection-in-Epoched-Data)
- [ARTIFACT REJECTION IN CONTINUOUS DATA](https://github.com/lucklab/erplab/wiki/Artifact-Rejection-in-Continuous-Data)
- [BEHAVIORAL ANALYSES](https://github.com/lucklab/erplab/wiki/Behavioral-Analyses)
- [COMPUTING AVERAGED ERPS](https://github.com/lucklab/erplab/wiki/Computing-Averaged-ERPs)
- [GETTING INFORMATION ABOUT AN ERP FROM THE MATLAB COMMAND LINE](https://github.com/lucklab/erplab/wiki/Getting-Information-about-an-ERP-from-the-Matlab-Command-Line)
- [ERP BIN OPERATIONS](https://github.com/lucklab/erplab/wiki/ERP-Bin-Operations)
- [EEG AND ERP CHANNEL OPERATIONS](https://github.com/lucklab/erplab/wiki/EEG-and-ERP-Channel-Operations)
- [FILTERING](https://github.com/lucklab/erplab/wiki/Filtering)
- [PLOTTING ERP WAVEFORMS](https://github.com/lucklab/erplab/wiki/Plotting-ERP-Waveforms)
- [TOPOGRAPHIC MAPPING](https://github.com/lucklab/erplab/wiki/Topographic-Mapping)
- [SAVING, LOADING, DUPLICATING, RENAMING, CLEARING, AND EXPORTING ERPSETS](https://github.com/lucklab/erplab/wiki/Saving,-Loading,-Duplicating,-Renaming,-Clearing,-and-Exporting-ERPSETS)
- [APPENDING ERPSETS](https://github.com/lucklab/erplab/wiki/Appending-ERPSETS)
- [AVERAGING ACROSS ERPSETS (CREATING GRAND AVERAGES)](https://github.com/lucklab/erplab/wiki/Averaging-Across-ERPSETS-(Creating-Grand-Averages))
- [ERP MEASUREMENT TOOL](https://github.com/lucklab/erplab/wiki/ERP-Measurement-Tool)
- [TIMING DETAILS](https://github.com/lucklab/erplab/wiki/Timing-Details)

Important note: The ERPLAB Discussion Forums have been retired. All comments and questions should be posted to the ERPLAB Email List.

Important note: In some cases, errors will occur leading to a message that instructs you to report the error to the EEGLAB developers.  If this happens, please report the error to us at erplab@erpinfo.org and not to the EEGLAB developers.

The purpose of this User's Manual is to provide a detailed description of the ERPLAB functions, along with a discussion of the overall design of the toolbox.  For "how-to" information, see the ERPLAB Tutorial, which provides step-by-step instructions for analyzing a typical set of data.  A [Frequently Asked Questions](https://github.com/lucklab/erplab/wiki/Troubleshooting-and-Frequently-Asked-Questions) document is also available.

If you have bug reports, requests for features, questions about using the software, and comments of general interest, please post them to the ERPLAB Email List.  To communicate privately with the developers, send an email to erplabtoolbox@gmail.com.

ERPLAB Toolbox is a freely available, open source set of MATLAB routines for analyzing event-related potential (ERP) data.  It uses the freely available, open source EEGLAB toolbox as a front end.  That is, EEGLAB is used to read in EEG data files and perform various operations on the EEG, and ERPLAB contains a set of new functions, which are added as plug-ins into EEGLAB, extending the set of operations that a user can perform within EEGLAB. These plug-ins include additional EEG processing manipulations (e.g., new functions for marking trials with artifacts) along with functions that provide powerful methods for sorting EEG epochs and averaging them together.  Once a set of averages has been created, they are saved in binary files and can be exported into text files (allowing them to be imported into other ERP analysis systems).

ERPLAB also contains a set of routines that operate on the averaged ERP waveforms (e.g., making difference waves, plotting, filtering, measurement, etc.). 

As in EEGLAB, the ERPLAB routines can be accessed from the Matlab command window and from Matlab scripts in addition to being accessed from the EEGLAB GUI. Consequently, ERPLAB provides the ease of learning of a GUI-based system but also provides the power and flexibility of a scripted system.