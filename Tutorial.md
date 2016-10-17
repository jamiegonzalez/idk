<h2 align="center">ERPLAB TOOLBOX TUTORIAL </h2>
<h5 align="center">
Version 4.0<br>
01 October 2013<br><br>
Tutorial written by Steve Luck, Javier Lopez-Calderon, Stan Huang, and Eric Foo <br><br>
ERPLAB Toolbox core designed by Javier Lopez-Calderon and Steve Luck<br><br>
</h5>

ERPLAB has primarily been tested using EEG collected with a Biosemi ActiveTwo System, along with a smaller amount of testing using EEG collected with Neuroscan and EGI systems. Consequently, you should be particularly careful when using this version of ERPLAB with data collected with systems other than the Biosemi ActiveTwo.

ERPLAB Toolbox is in a period of rapid development. Some features are present in this version that have not yet been documented, and some features may have changed since this document was released. In addition, some of the screen shots shown in this document may reflect previous versions and may not conform with the text.  The documentation, like the software, is a work in progress.

The goal of this tutorial is to provide step-by-step instructions for the processing of a typical data set.  For an overview of ERPLAB Toolbox and detailed information about each specific function, see the ERPLAB User's Manual. A Frequently Asked Questions document is also available.  All documentation is available at http://erpinfo.org/erplab/erplab-documentation.

If you have bug reports, requests for features, questions about using the software, and comments of general interest, please post them to the ERPLAB Email List.  To communicate privately with the developers, send an email to erplabtoolbox@gmail.com.

Please keep in mind that this is **FREE** software, and we do not have the resources to provide the level of support that commercial software vendors can provide.

## Table of Contents
---
1. [Overview and Scripting](./Overview-and-Scripting:-Tutorial)

2. [Getting Started](./Getting-Started:-Tutorial)

3. [Brief Description of the Example Experiment](./Brief-Description-of-the-Example-Experiment:-Tutorial)

4. [Adding Channel Locations to your Dataset](./Adding-Channel-Locations-to-your-Dataset:-Tutorial)

5. [Background Concepts: Datasets, ERPsets, and Bins](./Background-Concepts:-Datasets,-ERPsets,-and-Bins:-Tutorial)

6. [Creating an EventList](./Creating-an-EventList:-ERPLAB-Functions:-Tutorial)

7. [Advanced EventList Options](./Advanced-EventList-Options:-Tutorial)

8. [Creating Bin-Based EEG Epochs](./Creating-Bin--Based-EEG-Epochs:-Tutorial)

9. [Artifact Detection](./Artifact-Detection:-Tutorial)

10. [Creating Averaged ERPs](./Creating-Averaged-ERPs:-Tutorial)

11. [Plotting Averaged ERP Waveforms](./Plotting-Averaged-ERP-Waveforms:-Tutorial)

12. [Filtering EEG and ERPs](./Filtering-EEG-and-ERPs:-Tutorial)

13. [Combining ERP Waveforms with Bin Operations](./Combining-ERP-Waveforms-with-Bin-Operations:-Tutorial)

14. [Creating and Modifying Channels with Channel Operations](./Creating-and-Modifying-Channels-with-Channel-Operations:-Tutorial)

15. [Assigning Events to Bins with BINLISTER](./Assigning-Events-to-Bins-with-BINLISTER:-Tutorial:-Tutorial)

16. [Measuring amplitudes and latencies with the ERP Measurement Tool](./Measuring-amplitudes-and-latencies-with-the-ERP-Measurement-Tool:-Tutorial)

17. [Exporting and Importing EventLists to Combine Artifact Rejection and Artifact Correction](./Exporting-and-Importing-EventLists-to-Combine-Artifact-Rejection-and-Artifact-Correction:-Tutorial)