# ERPLAB TOOLBOX TUTORIAL
*Version 4.0* <br>
*01 October 2013*

Tutorial written by Steve Luck, Javier Lopez-Calderon, Stan Huang, and Eric Foo
<br><br>
ERPLAB Toolbox core designed by Javier Lopez-Calderon and Steve Luck
<br><br>
Important note: The ERPLAB Discussion Forums have been retired. All comments and questions should be posted to the ERPLAB Email List.
<br><br>
Important note: In some cases, errors will lead to a message that instructs you to report the error to the EEGLAB developers.  If this happens, please report the error to us at erplabtoolbox@gmail.com and not to the EEGLAB developers.

ERPLAB has primarily been tested using EEG collected with a Biosemi ActiveTwo System, along with a smaller amount of testing using EEG collected with Neuroscan and EGI systems. Consequently, you should be particularly careful when using this version of ERPLAB with data collected with systems other than the Biosemi ActiveTwo.

ERPLAB Toolbox is in a period of rapid development. Some features are present in this version that have not yet been documented, and some features may have changed since this document was released. In addition, some of the screen shots shown in this document may reflect previous versions and may not conform with the text.  The documentation, like the software, is a work in progress.

The goal of this tutorial is to provide step-by-step instructions for the processing of a typical data set.  For an overview of ERPLAB Toolbox and detailed information about each specific function, see the ERPLAB User's Manual. A Frequently Asked Questions document is also available.  All documentation is available at http://erpinfo.org/erplab/erplab-documentation.

If you have bug reports, requests for features, questions about using the software, and comments of general interest, please post them to the ERPLAB Email List.  To communicate privately with the developers, send an email to erplabtoolbox@gmail.com.

Please keep in mind that this is FREE software, and we do not have the resources to provide the level of support that commercial software vendors can provide.

Table of Contents

Overview and Scripting

Getting Started

Brief Description of the Example Experiment

Adding Channel Locations to your Dataset

Background Concepts: Datasets, ERPsets, and bins

Creating an EventList

Advanced EventList Options

Creating Bin-Based EEG Epochs

Artifact Detection

Creating Averaged ERPs

Plotting Averaged ERP Waveforms

Filtering EEG and ERPs

Combining ERP Waveforms with Bin Operations

Creating and Modifying Channels with Channel Operations

Assigning Events to Bins with BINLISTER

Measuring amplitudes and latencies with the ERP Measurement Tool

Exporting and Importing EventLists to Combine Artifact Rejection and Artifact Correction