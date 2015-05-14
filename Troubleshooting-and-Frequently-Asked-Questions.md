## Installation
I’ve just installed the latest release of ERPLAB, and only some of the functions work.  Other functions do not seem to work at all.  What is going on?
 
The Matlab path may not include the new ERPLAB functions. You must update the Matlab path by selecting File > Set Path from the Matlab command window.  Delete any old EEGLAB and ERPLAB folders from the path,  and re-adding the EEGLAB folder (and all subfolders) to the path by clicking on Add with subfolders and selecting the path to the EEGLAB folder (which contains the ERPLAB folders).  If you still have problems, you may want to clear all of the path information by clicking Default prior to clicking Add with subfolders.
 
Another possibility is that you don't have the Matlab Signal Processing Toolbox installed.  This must be installed for ERPLAB to work properly.  You can probably purchase this toolbox through your university's IT department (or you can buy it directly from the The Mathworks).
 
 
#### I have installed EEGLAB successfully, but ERPLAB does not show up in the EEGLAB window.  What is going on?
 
You may have put the ERPLAB folder in the wrong location.  The folder you downloaded should go inside the EEGLAB Plugins folder.  Your path should be something like this:
Applications > MATLAB> eeglab2008October01_beta >plugins>erplab_2.0.0.1
This folder should contain the ERPLAB files and folders.
 
A common error is to make an ERPLAB folder inside the plugins folder, and then place the downloaded folder inside this new folder, leading to a path like this:
Applications > MATLAB> eeglab2008October01_beta >plugins>erplab_2.0.0.1>erplab_2.0.0.1
 
Also, we recommend that you do not install EEGLAB inside the Toolbox folder of the Matlab application. Instead, we recommend that you install it somewhere inside your Documents folder (e.g., inside the Matlab folder within your Documents folder).
 
 
#### I’ve just installed the latest release of EEGLAB, and I get warning messages anytime I try to do anything in EEGLAB or ERPLAB.  What is going on?
 
The Matlab path may include a set of routines that are used to take the place of the Matlab Signal Processing Toolbox. To avoid this problem, update the Matlab path by selecting File > Set Path from the Matlab command window.  Delete any paths with external/fieldtrip in them and save.
 
## General Weird Problems
Things that worked before aren't working now.  Or most things work, but a few things generate error messages.  How can I fix this?
 
One likely explanation is that you haven't installed things properly or do not have the path set correctly.  You may want to reinstall EEGLAB and ERPLAB.
 
Another possibility is that you've upgraded to a new version of Matlab.  New versions sometimes change core functions, leading to problems with ERPLAB.  It generally takes us several months to release a new version of ERPLAB after Matlab has been updated.
 
A third possibility is that ERPLAB's "working memory" has become corrupted.  This is the memory that stores all the parameters that you've specified in your various windows.  You can reset the working memory by selecting ERPLAB > Settings > Reset ERPLAB's Working Memory.
 
## How do I replace a bad channel with interpolated data?
 
This is done with EEG Channel Operations (see the Channel Operations page in the ERPLAB User's Manual).
 
## How do I make contra and ipsi waveforms (for N2pc, CDA, LRP, etc.)
 
This is done with ERP Bin Operations (see the ERP Bin Operations page in the ERPLAB User's Manual).
 
## Problems with missing events (especially in Brain Products or EGI systems)
ERPLAB does not seem to recognize my event markers.  For example, when I run BINLISTER, it can't find any events that match my bin descriptors.
 
The problem is that text strings are being used for the event markers (e.g., "S4"), and ERPLAB requires numeric values.  You can convert each string to a number using the Advanced version of Create EventList.  Alternatively, if your event markers contain both numeric and non-numeric information (e.g., 'S21'), you can use a function called letterkilla to strip out the non-numeric information. From the Matlab command window or a script, you will type EEG = letterkilla(EEG); You can then type eeglab redraw to make the updated dataset available from the EEGLAB GUI.  More recent versions of ERPLAB have an option in the Create EventList GUI for removing non-numeric information.
 
## Speed
Some operations are very slow.  How can I make ERPLAB run faster?
 
Matlab is very fast for some kinds of operations and very slow for others.  BINLISTER, in particular, can be very slow.  Sometimes this is because you have many irrelevant event codes in your EventList.  You can tell BINLISTER to ignore these events, which may make it work faster.
 
If everything seems slow (especially loading files), you may have insufficient memory.   We recommend at least 8 GB of RAM. Note, however, that your computer will not be able to take advantage of more than 4 GB of RAM unless you have a 64-bit version of Matlab installed (along with a 64-bit operating system).
 
## Plotting ERPs
I would like to create a single plot that overlays the waveforms from different files.  How do I do this?
 
In the current version of ERPLAB, it is not possible to directly plot waveforms from different ERPsets in the same plot. To accomplish this, you can append one ERPset onto the end of another ERPset with ERPLAB > Append ERPsets.  This will create a new ERPset that has twice as many bins (all the bins from the first ERPset followed by all the bins from the second ERPset).  You can then overlay the bins corresponding to the original first and second ERPsets.  (We will create an easier method for this in a future version of ERPLAB.)
 
## Plotting EEG
I have just imported my data, and I tried looking at it with EEGLAB's plot scrolling data function, and I cannot see any (or some) of my channels.  What is wrong?
 
You probably recorded at DC, and many or all of your channels may have a large DC offset that puts them out of the range of values shown in the window.  You can solve this by: (1) high-pass filtering your data before plotting; or (2) In the Plot > Channel data (scroll) window, increase the scaling value so that a broader range of values is plotted;l or (3)  In the Plot > Channel data (scroll) window, go to 'Display' menu -> 'Remove DC offset'.
 
## Importing Epoched Data
I have already epoched my data in EEGLAB.  Is it possible to add an EventList to a dataset that was epoched using EEGLAB?
 
Not usually (see next question for a trick).  To use most ERPLAB functions, you must create the EventList in the continuous data and use ERPLAB's "bin epoching" function to epoch your data.  ERPLAB creates links between the EventList and the event information in the continuous data, and many ERPLAB functions would "break" if we tried to create an EventList on an epoched dataset.  The next answer also provides a trick that works in many cases.  If this does not work, you may need to write your own scripts to do this.
 
I want to use BINLISTER on data that have already been epoched (in EEGLAB or ERPLAB).  Is there any way to do this?
 
There is a trick for this that may work.  Try using ERPLAB > Utilities > Convert an epoched dataset into a continuous one. This creates a "fake" continuous dataset, with "boundary" events between the epochs. This doesn't always solve the problem, but it does in many cases.
 