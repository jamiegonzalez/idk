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
- IMPORTANT BACKGROUND CONCEPTS AND DATA STRUCTURES
- USING EEGLAB
- THE EVENTLIST STRUCTURE
- CREATING AN EVENTLIST
- EXPORTING, EDITING, AND IMPORTING EVENTLISTS

Boundary Events and Disabled Events

- ASSIGNING EVENTS TO BINS WITH BINLISTER
- EPOCHING BINS
- ARTIFACT DETECTION IN EPOCHED DATA
- ARTIFACT REJECTION IN CONTINUOUS DATA
- BEHAVIORAL ANALYSES
- COMPUTING AVERAGED ERPS
- GETTING INFORMATION ABOUT AN ERP FROM THE MATLAB COMMAND LINE
- ERP BIN OPERATIONS
- EEG AND ERP CHANNEL OPERATIONS
- FILTERING
- PLOTTING ERP WAVEFORMS
- TOPOGRAPHIC MAPPING
- SAVING, LOADING, DUPLICATING, RENAMING, CLEARING, AND EXPORTING ERPSETS
- APPENDING ERPSETS
- AVERAGING ACROSS ERPSETS (CREATING GRAND AVERAGES)
- ERP MEASUREMENT TOOL
- TIMING DETAILS

Important note: The ERPLAB Discussion Forums have been retired. All comments and questions should be posted to the ERPLAB Email List.

Important note: In some cases, errors will occur leading to a message that instructs you to report the error to the EEGLAB developers.  If this happens, please report the error to us at erplab@erpinfo.org and not to the EEGLAB developers.

The purpose of this User's Manual is to provide a detailed description of the ERPLAB functions, along with a discussion of the overall design of the toolbox.  For "how-to" information, see the ERPLAB Tutorial, which provides step-by-step instructions for analyzing a typical set of data.  A Frequently Asked Questions document is also available.

If you have bug reports, requests for features, questions about using the software, and comments of general interest, please post them to the ERPLAB Email List.  To communicate privately with the developers, send an email to erplabtoolbox@gmail.com.

ERPLAB Toolbox is a freely available, open source set of MATLAB routines for analyzing event-related potential (ERP) data.  It uses the freely available, open source EEGLAB toolbox as a front end.  That is, EEGLAB is used to read in EEG data files and perform various operations on the EEG, and ERPLAB contains a set of new functions, which are added as plug-ins into EEGLAB, extending the set of operations that a user can perform within EEGLAB. These plug-ins include additional EEG processing manipulations (e.g., new functions for marking trials with artifacts) along with functions that provide powerful methods for sorting EEG epochs and averaging them together.  Once a set of averages has been created, they are saved in binary files and can be exported into text files (allowing them to be imported into other ERP analysis systems).

ERPLAB also contains a set of routines that operate on the averaged ERP waveforms (e.g., making difference waves, plotting, filtering, measurement, etc.). 

As in EEGLAB, the ERPLAB routines can be accessed from the Matlab command window and from Matlab scripts in addition to being accessed from the EEGLAB GUI. Consequently, ERPLAB provides the ease of learning of a GUI-based system but also provides the power and flexibility of a scripted system.