# Getting started
We assume that Matlab is installed, that EEGLAB is installed and in the Matlab path, and that ERPLAB is correctly installed in the EEGLAB plugin subfolder. If not, see the [installation instructions here](https://github.com/lucklab/erplab/wiki/Installation).

<TABLE>
   <TR>
     <TH>Requirements</TH>
     <TH>Completed?</TH>
   </TR>
   <TR>
      <TD> <a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#load-eeg-data-in-to-eeglab"> Load EEG Data </a> </TD>
      <TD align="center">  </TD>
   </TR>
   <TR>
      <TD> <a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#events-and-the-eventlist"> Creating an EventList </a> </TD>
      <TD align="center">  </TD>
   </TR>
 <TR>
      <TD> <a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#assigning-trials-to-bins"> Assigning Trials to Bins </a> </TD>
      <TD align="center">  </TD>
   </TR>
   <TR>
      <TD><a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#extract-bin-based-epochs">  Creating Bin-Based EEG Epochs </a></TD>
      <TD align="center">  </TD>
   </TR>
<TR>
      <TD><a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#artifact-detection"> Artifact Detection </a></TD>
      <TD align="center">  </TD>
   </TR>
<TR>
      <TD><a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#create-averaged-ERPs"> Creating Averaged ERPs </a></TD>
      <TD align="center">  </TD>
   </TR>
</TABLE>

## Download example EEG data set

Download the [example EEG data files here](https://ucdavis.box.com/shared/static/f1go6b880w82cle1l53pucvsymcbp4st.zip). Unzip to a known folder, here we show `C:\m\eegdata\erplab_tut`. Note that there is a subfolder for each experiment subject, S1 to S6.

![Tut_data_folder2](https://user-images.githubusercontent.com/5137405/83183516-c49b9000-a0dc-11ea-89d0-64834b883ade.png)

Within the `S1` subfolder, you the `S1_EEG.set` file. This file contains the continuous EEG data for subject 1 in EEGLAB format, and also includes some meta data, like the event code timing information.


### Run Matlab, and enter `eeglab` in the Matlab Command Window.

You should see something close to these screenshots. :

Matlab environment, entering `eeglab` in the Command Window

<a href="https://user-images.githubusercontent.com/5137405/82972479-ffd97a00-9f89-11ea-9464-93a29d0bafa1.png">
 <img src="https://user-images.githubusercontent.com/5137405/82972479-ffd97a00-9f89-11ea-9464-93a29d0bafa1.png" alt="Matlab_env - click for bigger image";
style="cursor:pointer;"
     title="Matlab_env - click for bigger image">
</a>


A new window appears for EEGLAB, with the ERPLAB menu:

<a href="https://user-images.githubusercontent.com/5137405/82972482-010aa700-9f8a-11ea-8290-0231c5d1abb9.png">
 <img src="https://user-images.githubusercontent.com/5137405/82972482-010aa700-9f8a-11ea-8290-0231c5d1abb9.png" alt="Matlab_env_with_ERPLAB - click for bigger image";
style="cursor:pointer;"
     title="Matlab_env_with_ERPLAB - click for bigger image">
</a>

If you encounter an error here, check that ERPLAB is installed correctly, and the troubleshooting hints.


## Load EEG data in to EEGLAB

With EEGLAB started within Matlab, hit `File > Load existing dataset`.

![Load_EEGset](https://user-images.githubusercontent.com/5137405/83186512-7a68dd80-a0e1-11ea-95f3-5de5f7a20377.png)

Select the `S1_EEG.set` file, from the `S1` subfolder in the path you unzipped example EEG data to.

The EEGLAB window should now update to show some information about this loaded EEG set:
![S1_loaded_dataset_list](https://user-images.githubusercontent.com/5137405/83187297-cd8f6000-a0e2-11ea-8c2e-93f942020cde.png)

Also, a list of currently loaded EEG sets is shown in the EEGLAB window as a dropdown menu, now containing `Dataset 1: S1_EEG`. There is also dropdown menu for `ERPsets`, and this remains empty, as we have only loaded continuous EEG data.



## Get to know your EEG data
There are several aspects to the EEG datasets that are good to keep in mind. As these can be observed and verified here, it is good practice to do so at this stage:

* What data do I have? How many EEG channels? What is the duration of the recording?

This can be found within the blue EEGLAB GUI (as shown in screenshots above), where the channels per frame tells you the number of channels. The number of epochs is 1, the epoch start time is 0, and the epoch end time is 2139 s, indicating that the loaded and currently selected EEG set is continuous data, and runs from t=0 s to t=2139 s, giving (2139/60) around a 35 minute recording. This is EEG data recorded at a sample rate of 500 Hz, so there are (2139 * 500) around 1,069,500 datapoints for each electrode. 

This information can also be accessed programatically within Matlab, with commands like: 
`EEG.nbchan` `size(EEG.data)` `EEG.srate`


* What events occur within this recording? Are there event codes (aka event markers, triggers) indicating the relevant times of stimuli presentation and response?

From the EEGLAB window, we can plot the EEG recording data, through `Plot menu -> Channel data (scroll)`.

![Plot_EEG](https://user-images.githubusercontent.com/5137405/83189862-68d60480-a0e6-11ea-8c72-a2bf996ea5e2.png)

Channel data is presented with one channel atop another, with channel F3 on top here. If you advance the time from 0 s to 10 s, you can observe two large deflections of more that 50 µV that occur at around 10.5 s and 12 s. These are likely blinks.

![Plot_EEG_scroll](https://user-images.githubusercontent.com/5137405/83190634-953e5080-a0e7-11ea-86c5-541fdd16bd59.png)

Additionally, there are straight vertical dashed lines, of different colors. There are none of these in the first 12 seconds of this recording, and 4 in the trace shown above, at around 13.1, 13.6, 14.3, and 14.8 seconds. These are the event codes, indicating an event of type 22, 9, 12, 9 occurred at the respective times.

These event codes have been generated by the experimental stimuli script at the time of recording the EEG, and included with the EEG data. The 22 indicates the presentation of a certain type of frequently shown stimulus, the 12 indicates a certain type of rarely shown stimulus, and 9 indicates the time at which the subject made a buttonpress response. Here, we wish to observe that this data exists, and agrees with our expectations of this experiment.

This information can also be accessed programatically within Matlab, with commands like: 
`pop_squeezevents(EEG)`

![Count_events](https://user-images.githubusercontent.com/5137405/83191773-6e811980-a0e9-11ea-9ad8-54ce484dc510.png)



* What ERPs are desired? What timeframe is desired to show these ERPs?

Your research question will determine what the ERP and timeframes that are central for your experiment. Hopefully, your experimental design captures this ERP component well. There exists guides to help, like the [Oxford Handbook of ERPs](https://www.oxfordhandbooks.com/view/10.1093/oxfordhb/9780195374148.001.0001/oxfordhb-9780195374148) for example.


Now that we have loaded and examined some data, the next step is to attach an EventList:

<TABLE>
   <TR>
     <TH>Requirements</TH>
     <TH>Completed?</TH>
   </TR>
   <TR>
      <TD> <a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#load-eeg-data-in-to-eeglab"> Load EEG Data </a> </TD>
      <TD align="center"> &#10003 </TD>
   </TR>
   <TR>
      <TD> <a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#events-and-the-eventlist"> Creating an EventList </a> </TD>
      <TD align="center">  </TD>
   </TR>
 <TR>
      <TD> <a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#assigning-trials-to-bins"> Assigning Trials to Bins </a> </TD>
      <TD align="center">   </TD>
   </TR>
   <TR>
      <TD><a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#extract-bin-based-epochs">  Creating Bin-Based EEG Epochs </a></TD>
      <TD align="center">   </TD>
   </TR>
<TR>
      <TD><a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#artifact-detection"> Artifact Detection </a></TD>
      <TD align="center"> </TD>
   </TR>
<TR>
      <TD><a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#create-averaged-ERPs"> Creating Averaged ERPs </a></TD>
      <TD align="center">  </TD>
   </TR>
</TABLE>
<br><br>

# Events and the Eventlist

At the moment, this dataset is continuous EEG data, with event markers indicating the times of trial-relevant stimulus presentation.

In order to turn this data into an Averaged ERP dataset, we need to keep track of these events in an ERPLAB format EventList, and then determine what events should go in what bin of the ERP.

Here, we wish to group the Frequent stimuli type together in one bin, and the Rare stimuli type in another, to show the difference in their averages in a P300 ERP. For more information about the experiment, [see here](https://github.com/lucklab/erplab/wiki/Brief-Description-of-the-Example-Experiment:-Tutorial).

The EventList is a refactoring of the trial information in a more ERPLAB-interpretable way, so we can address these events later on.

The current stimulus event codes (as seen with `pop_squeezevents(EEG)`) is:


    Event Code	  Category      Probability     Correct Response
    11	          Letter        Frequent        Left Hand
    21	          Digit         Rare            Right Hand
    112	          Letter        Rare            Left Hand
    122	          Digit         Frequent        Right Hand
    12	          Letter        Rare            Right Hand
    22	          Digit         Frequent        Left Hand
    111	          Letter        Frequent        Right Hand
    121	          Digit         Rare            Left Hand
 

### Creating an Eventlist
To create an EventList for the EEG data we loaded above, let's hit <br>
`ERPLAB menu > EventList > Create EEG EVENTLIST`


![Create_EL](https://user-images.githubusercontent.com/5137405/84070306-c6890d00-a980-11ea-93c5-85a6090aa7de.png)

That will pop up this new window. Optionally, we can write the EL to a text file. The information will still be 'attached' to this EEGset, but that text file can be useful for examining outside Matlab.

#### Stick to numeric events - not strings
Note that the EventList does not like strings. Event names are best to be numbers and not text. If your event names are text, we suggest converting them to a numeric code here. The events here are all numbers, but stored as stings for now. Using the 'Create numeric equivilent' option in the 'Create EventList' GUI, the text is dropped from a string event code, leaving the number. This option will trim any text, and convert to numeric type, and so will work for these event codes. If you need to convert different types of string events to numeric, you can use the 'Convert string code' editable option in the middle of this window, but this is not needed for this example dataset.

The boundary code is an important event code, indicating the presence of a discontinuity, like a removed section of data, or a break in the recording. We recommend keeping that in the data with the numeric indicator of event `-99`.

![create_eventlist_window](https://user-images.githubusercontent.com/5137405/84316905-cc1d5900-ab20-11ea-87af-03b534022098.png)
 
After hitting 'CREATE', a new EEG set is created -- same as the previous one, but now with a EventList attached.

Let's save this new EEG set in the S1 folder.

#### Looking at the EventList
Optionally, to inspect this new EL, we can probe

`EEG.EVENTLIST.eventinfo`

or explore there in the Matlab Workspace.

![EEG_EL_struct](https://user-images.githubusercontent.com/5137405/84317286-64b3d900-ab21-11ea-9737-1a0d0ec08fd8.png)


If you chose to write the EventList to a text file, you can also view it in the Matlab editor with something like:
`edit S1/EventList_1.txt`

This shows our events (all 2557 of them), and the time that they occurred.

Note that at the moment, the code field is filled, and that the binlabel field is empty.

<TABLE>
   <TR>
     <TH>Requirements</TH>
     <TH>Completed?</TH>
   </TR>
   <TR>
      <TD> <a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#load-eeg-data-in-to-eeglab"> Load EEG Data </a> </TD>
      <TD align="center"> &#10003 </TD>
   </TR>
   <TR>
      <TD> <a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#events-and-the-eventlist"> Creating an EventList </a> </TD>
      <TD align="center"> &#10003 </TD>
   </TR>
 <TR>
      <TD> <a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#assigning-trials-to-bins"> Assigning Trials to Bins </a> </TD>
      <TD align="center">   </TD>
   </TR>
   <TR>
      <TD><a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#extract-bin-based-epochs">  Creating Bin-Based EEG Epochs </a></TD>
      <TD align="center">   </TD>
   </TR>
<TR>
      <TD><a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#artifact-detection"> Artifact Detection </a></TD>
      <TD align="center"> </TD>
   </TR>
<TR>
      <TD><a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#create-averaged-ERPs"> Creating Averaged ERPs </a></TD>
      <TD align="center">  </TD>
   </TR>
</TABLE>
<br><br>



# Assigning Trials to Bins

With the events coded in the EventList, we can now specify what we want in ERP bins.

We have event codes for different 'frequent' or 'rare' stimuli presentation times. For this P300 experiment, we wish to group all the 'frequent' stimuli in to one bin, and the rare in to another, so they can then be averaged together and compared in in ERP set.

From the design of this experiment, we know that all of {11,122,22,111} event codes indicate Frequent stimuli, and that all of {21,112,12,121} are Rare stimuli. Additionally, an event code of {9} indicates a correct response.

The syntax of BINLISTER allows specification of bins for complex experiments. Here, we will go for a simple example, but I hope I can show you how it might be powerful.

The idea is to set instruction for each bin in a specific format, called the Bin-Descriptor Files:

````
bin 1
Frequent followed by correct response
.{11;122;22;111}{9}

bin 2
Rare followed by correct response
.{21;112;12;121}{9}  

````

These Bin-Descriptor Files are saved as raw text files, and used by ERPLAB's BinLister function to specify ERP bins. You can see an example of these files in the `Test_Data/binlister_demo_1.txt` file. Open this file with the Matlab text editor by right-clicking it in the Matlab 'Current Folder' section, or through `edit binlister_demo_1.txt` if you are in the Test_Data directory. Using MS Word to edit these files can add incorrect formatting, so we recommend using the Matlab editor (or, perhaps, another raw text editor like [Sublime Text](https://www.sublimetext.com/).

#### Unpacking BDF syntax
Note that there are exactly 3 lines for each bin, followed by an empty line, like:

bin <number_n> <br>
Text name of bin <br>
.{1;2}{3} <br>
<empty line> <br>
<br>
Let's unpack that.
The bin numbers start at 1, and go up by 1.
The text name of the bin is specified by you. Make it unique and descriptive.

The event specification is in the 3rd line. Each curly brackets {} give an event set, that contains at least 1 event. The period immediately precedes the event set that will become the 'anchor' event, being time zero (=== 0 ms) for the resulting bin.

If event codes are seperated by semi-colons an event set, like .{1;2} that means that any one of the those event codes are valid for a match in that position. When one set of events in curly brackets follows another, there must be a match for the first set IMMEDIATELY followed by a match for the next. Any time in the continuous EEG trace time that there is an:
 event code 1 followed by event code 3 
 OR
 event code 2 followed by event code 3

there is then a match for this bin specification, and so this could go in to bin n.

So if there were a train of 3 events in the continuous EEG trace of:
1---3
..that would be captured by the above bin specification.

And
1--5--3
would not be captured by this bin specification, as there is an intervening event code of 5 in between the 1 and the 3.


#### Applying Bin-Descriptors to EEG dataset
With both an EventList and Bin-Descriptor file, we can run BINLISTER to apply that Bin-Descriptor to the loaded EEG dataset. 

`ERPLAB menu -> Assign bins (BINLISTER)`

![Binlister_GUI](https://user-images.githubusercontent.com/5137405/84330206-a5205080-ab3b-11ea-9473-f52d17e12294.png)

In the top section, hit 'Browse' and select the `binlister_demo_1.txt` file. Optionally, you can hit 'Take a look' to verify that this is the bin-descriptor you want.

On hitting 'RUN' on this window, BinLister will examine all the events, and, when there is a match to any of the requested bins, add this information to the EventList. This will create a new EEG dataset, now with the suggested name appended with '_bins', so 'S1_EEG_elist_bins' by default for our first subject here.

If we examine the EEG.EVENTLIST.eventinfo structure in this new EEG data in the Matlab Workspace variable explorer, we can see the updated EventList, now with bin info. For instance, the binlabel field for the first item now shows that it will be grouped to Bin 1, as it has a 22 event code that is immediately followed by a 9. The binlabel for the third item shows it has been has a Bin 2 label, as it was a 12 event code followed by a 9.


<TABLE>
   <TR>
     <TH>Requirements</TH>
     <TH>Completed?</TH>
   </TR>
   <TR>
      <TD> <a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#load-eeg-data-in-to-eeglab"> Load EEG Data </a> </TD>
      <TD align="center"> &#10003 </TD>
   </TR>
   <TR>
      <TD> <a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#events-and-the-eventlist"> Creating an EventList </a> </TD>
      <TD align="center"> &#10003 </TD>
   </TR>
 <TR>
      <TD> <a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#assigning-trials-to-bins"> Assigning Trials to Bins </a> </TD>
      <TD align="center"> &#10003  </TD>
   </TR>
   <TR>
      <TD><a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#extract-bin-based-epochs">  Creating Bin-Based EEG Epochs </a></TD>
      <TD align="center">   </TD>
   </TR>
<TR>
      <TD><a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#artifact-detection"> Artifact Detection </a></TD>
      <TD align="center"> </TD>
   </TR>
<TR>
      <TD><a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#create-averaged-ERPs"> Creating Averaged ERPs </a></TD>
      <TD align="center">  </TD>
   </TR>
</TABLE>
<br><br>


# Extract bin-based epochs
Now that the bin information is present, we can convert this continuous EEG dataset into a series of short stretches of data oriented around key events, making an epoched EEG set. For all periods of the EEG data that match one of the above-defined bins, we will take a period of time around the defined event (typically around 200 ms before and 800 ms after), and that will be an epoch. Epochs will be anchored around specific event markers, with some time before and after. Rather than the previous continuous EEG data stored in the format of

` (number of electrodes) * (number of time-points) `

epoched EEG data will now be stored in the format of 

`(number of electrodes) * (number of time-points in epoch) * (number of epochs/trials) `

Running the command of `size(EEG.data)` on our existing EEG set reveals a 16 electrode by 1 million datapoint 2D data array.

To extract bin-based epochs, hit:
`ERPLAB menu -> Extract bin-based epochs`

![extract_bin_epochs](https://user-images.githubusercontent.com/5137405/84331649-a2275f00-ab3f-11ea-9e17-7415ad2b5aad.png)

We specify the time range in the top section -- here, -200 up to 800 ms. This means each epoch will be 1000 ms long. Note that this is in milliseconds, relative to the event specified with a leading period in the bin-descriptor file, like `.{11}`. 

Hitting 'Run' here will create a new EEG dataset, with the now-epoched data. To indicate that this is bin-epoched data, the suggested name of the EEG set will be appended with '_be', giving `S1_EEG_elist_bins_be` if you have followed all steps so far.

You can confirm that this data is now epoched by seeing that the blue EEGLAB window now lists 'Epochs:   1251'. This tells us that from the around 2500 events present in this EEG dataset, there are 1251 matches for the bins that we specified with the BDF above.


![EEGLAB_post_binepoch](https://user-images.githubusercontent.com/5137405/84332074-cafc2400-ab40-11ea-94de-442579e46cb6.png)

Additional confirmation can be seen by entering the command of `size(EEG.data)` again, reveals a 16 electrode by 500 datapoints by 1251 epoch 3D data array. Note that 1 second of data at 500 Hz gives 500 datapoints per epoch.

<TABLE>
   <TR>
     <TH>Requirements</TH>
     <TH>Completed?</TH>
   </TR>
   <TR>
      <TD> <a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#load-eeg-data-in-to-eeglab"> Load EEG Data </a> </TD>
      <TD align="center"> &#10003 </TD>
   </TR>
   <TR>
      <TD> <a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#events-and-the-eventlist"> Creating an EventList </a> </TD>
      <TD align="center"> &#10003 </TD>
   </TR>
 <TR>
      <TD> <a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#assigning-trials-to-bins"> Assigning Trials to Bins </a> </TD>
      <TD align="center"> &#10003  </TD>
   </TR>
   <TR>
      <TD><a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#extract-bin-based-epochs">  Creating Bin-Based EEG Epochs </a></TD>
      <TD align="center"> &#10003  </TD>
   </TR>
<TR>
      <TD><a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#artifact-detection"> Artifact Detection </a></TD>
      <TD align="center"> </TD>
   </TR>
<TR>
      <TD><a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#create-averaged-ERPs"> Creating Averaged ERPs </a></TD>
      <TD align="center">  </TD>
   </TR>
</TABLE>
<br><br>


# Artifact Detection
At this point, it would be possible to average these epochs into their respective bins, forming an ERP set. Before doing so, we can improve the data quality of our ERPs by marking epochs that have obvious artifacts.

For example, if we look at the first 5 epochs of the now-epoched EEG trace (through `Plot menu -> Channel Data scroll`), we can see that a large deflection exists at around 550 ms in to epoch 5. This is probably due to the subject blinking. We can see that there are also such artifacts in epoch 8 and 11, and in more epochs too. If we were to average this data without marking and excluding these epochs, these large non-neural deflections would add to the noise of our ERP results.

![EEG_trace_bin_epochs](https://user-images.githubusercontent.com/5137405/84417790-ffb4bd80-abca-11ea-8c93-fe358aa63331.png)


#### Artifact detection, not artifact obliteration
ERPLAB has several tools for detecting and marking different types of artifacts. Note that these tools will *mark* epochs as identified as being an artifact. This does not remove data from the EEG set, but instead allows these to then easily be excluded from the epochs that go into an ERP bin. This is contrasted with some EEGLAB *artifact rejection* functions, which will delete and remove sections from the EEG set.

If you do perform EEGLAB *artifact rejection*, be sure to regenerate a ERPLAB EventList afterwards.


### Moving Window Peak-to-Peak Detection
Many types of artifacts can be detected with ERPLAB's moving window peak-to-peak tool.

Hit `ERPLAB menu -> Artifact detection in epoched data -> Moving window peak-to-peak threshold `

This will open a new window, where we can specify parameters for this artifact detection method. This function will has a small window of analysis that steps through the time if the epochs, and records the difference between the point of lowest and highest amplitude. If this is ever above a stated threshold, the whole epoch is marked as an artifact. For more details, hit `?` in the window, or see the [ERPLAB manual page here](https://github.com/lucklab/erplab/wiki/Artifact-Detection-in-Epoched-Data).

![AR_mov_windows_p2p](https://user-images.githubusercontent.com/5137405/84423597-8bcae300-abd3-11ea-9528-cd390f1de89e.png)

By default, the 'test period' will be the whole epoch, stated in milliseconds. We go with the default moving window size of 200 ms, with 100 ms step size. The 'Voltage Threshold [µV]' is a key parameter, that may change across your subjects. For more sensitivity, lower this threshold, and more epochs will be found to be above this. For capturing the large blinks in S1 here, a value of 100 µV might be sensible.

Note that there are also 'flags' which can be used to disambiguate what artifact detection tools marked which epochs. The F1 flag is active for all artifacts, and, optionally, you can select others too. Here, Let's press the flag 2 button, so that both F1 and F2 are marked. 

Hitting 'Accept' here will run this artifact detection tool with these parameters, and create a new epoched EEG set with those matching epochs marked as artifacts. By default, '_ar'will be appended to the EEG set name, giving 'S1_EEG_elist_bins_be_ar' for our new EEG set.

ERPLAB will also output a summary of the artifact detection operation:

![AR_report](https://user-images.githubusercontent.com/5137405/84424694-51fadc00-abd5-11ea-9ada-f0bfa3e915a9.png)

Note that 288 epochs are now tagged as artifacts from Bin 1, and 72 from Bin 2. This is around 29% of trials from each bin now tagged as artifacts (which is a large but not crazy fraction), leaving 721 trials with now artifact tag in Bin 1, and 170 in Bin 2. You can examine this artifact summary again through `pop_summary_AR_eeg_detection(EEG);` or `ERPLAB menu -> Summarize artifact detection `.

Examining the EEG trace after this artifact detection process (through `EEGLAB Plot menu -> Channel data (scroll)`) reveals that many epochs with large artifacts are now highlighted in yellow. That includes the epoch 5, 8, and 11, which we previously noted as having likely blink artifacts.

![EEG_trace_bin_epoch_ar](https://user-images.githubusercontent.com/5137405/84425465-7a370a80-abd6-11ea-95c6-c78ebe801478.png)

Additional artifact detection routines can be run to find more artifacts, and have more accurate detection. See the [ERPLAB manual page here](https://github.com/lucklab/erplab/wiki/Artifact-Detection-in-Epoched-Data).

<TABLE>
   <TR>
     <TH>Requirements</TH>
     <TH>Completed?</TH>
   </TR>
   <TR>
      <TD> <a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#load-eeg-data-in-to-eeglab"> Load EEG Data </a> </TD>
      <TD align="center"> &#10003 </TD>
   </TR>
   <TR>
      <TD> <a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#events-and-the-eventlist"> Creating an EventList </a> </TD>
      <TD align="center"> &#10003 </TD>
   </TR>
 <TR>
      <TD> <a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#assigning-trials-to-bins"> Assigning Trials to Bins </a> </TD>
      <TD align="center">  &#10003  </TD>
   </TR>
   <TR>
      <TD><a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#extract-bin-based-epochs">  Creating Bin-Based EEG Epochs </a></TD>
      <TD align="center">  &#10003 </TD>
   </TR>
<TR>
      <TD><a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#artifact-detection"> Artifact Detection </a></TD>
      <TD align="center"> &#10003 </TD>
   </TR>
<TR>
      <TD><a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#create-averaged-ERPs"> Creating Averaged ERPs </a></TD>
      <TD align="center"> </TD>
   </TR>
</TABLE>

<br>

# Create Averaged ERPs
The final step here is to actually run the Averager, taking this processed epoched EEG set, and outputting and Averaged ERP dataset.

Hit: <br>
`ERPLAB menu -> Compute averaged ERPs`

![ERPLAB_ERP_Averager_GUI](https://user-images.githubusercontent.com/5137405/84427853-6c838400-abda-11ea-811e-7412d3c92f59.png)

At the top, we see the selected EEG dataset is number 5, which corresponds to the active EEG dataset here - S1_EEG_elist_bins_ar.

In the central section here, we specify that we wish to exclude epochs marked as artifacts. There are also options for selecting different sets of epochs, but we want all non-artifact epochs here. There is also an option for excluding any epoch that has boundaries or invalid events. We recommend having this tickbox enabled, so as to ignore epochs with boundary edge effects.

By default, we also have automatic data quality assessment enabled, with default options. This will include information about baseline noise, SEM, and Standardized Measurement Error (aSME) in the ERPset (see [more details for these options here](https://github.com/lucklab/erplab/wiki/ERPLAB-Data-Quality-Metrics)).

Hitting 'Run' here will create a ERP dataset.

This will pop up the 'Save ERPset GUI' for the first time. Let's save this as 'S1_ERP', and also save this new ERPset to a file, within the S1 subject folder:

![save_erpset](https://user-images.githubusercontent.com/5137405/84432433-a73cea80-abe1-11ea-9ee7-c73f297b2be5.png)


#### Reminder on EEG sets and ERP sets
With this new ERPset created, we now have an active ERPset that is selected. Alongside the EEGLAB 'Datasets' menu, which shows the 5 EEGsets from S1, we also have an 'ERPsets' menu, which shows the loaded ERPsets: <br>
`ERPset 1: S1_ERP` <br>

![ERPset_menu](https://user-images.githubusercontent.com/5137405/84432994-76a98080-abe2-11ea-9133-9546d38b4409.png)

Averaging each bin in the above bin-epoched EEG data give us ERP data in the format:

` (number of electrodes) * (number of time-points in epoch) * (number of bins) `

With the data prepared in this ERP set, we can access and plot the data from each condition:

![ERP_Viewer2](https://user-images.githubusercontent.com/5137405/82585605-1b3c2380-9b4b-11ea-938a-91def4b6684d.png)



<TABLE>
   <TR>
     <TH>Requirements</TH>
     <TH>Completed?</TH>
   </TR>
   <TR>
      <TD> <a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#load-eeg-data-in-to-eeglab"> Load EEG Data </a> </TD>
      <TD align="center"> &#10003 </TD>
   </TR>
   <TR>
      <TD> <a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#events-and-the-eventlist"> Creating an EventList </a> </TD>
      <TD align="center"> &#10003 </TD>
   </TR>
 <TR>
      <TD> <a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#assigning-trials-to-bins"> Assigning Trials to Bins </a> </TD>
      <TD align="center">  &#10003  </TD>
   </TR>
   <TR>
      <TD><a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#extract-bin-based-epochs">  Creating Bin-Based EEG Epochs </a></TD>
      <TD align="center">  &#10003 </TD>
   </TR>
<TR>
      <TD><a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#artifact-detection"> Artifact Detection </a></TD>
      <TD align="center"> &#10003 </TD>
   </TR>
<TR>
      <TD><a href="https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#create-averaged-ERPs"> Creating Averaged ERPs </a></TD>
      <TD align="center"> &#10003 </TD>
   </TR>
</TABLE>

<br>

We have a loaded ERPset! We can now run the many ERPLAB functions that act on this ERPset, including plotting and measuring tools.

We demonstrate use of some of these tools in the next tutorial.



<!--Bottom Navigation HTML-->
<br><br><br><br>
----
<table >
  <tr>
    <td  align="right" width="40%">
<a href=https://github.com/lucklab/erplab/wiki/ERPLAB-Tutorial#tutorial-table-of-contents>
        <img src="https://github.com/lucklab/erplab/wiki/images/ionicicons/ios7-arrow-back.png" alt="back arrow" height="75">
        <br>
        Tutorial Overview
      </a>
    </td>
    <td  align="center" width="20%">
      <a href="https://github.com/lucklab/erplab/wiki/ERPLAB-Tutorial#tutorial-table-of-contents">
        <img src="https://github.com/lucklab/erplab/wiki/images/ionicicons/ios7-copy.png" alt="tutorial icon" height="75">
        <br>
        Tutorial list
       </a>
    </td>
    <td  align="left" width="40%">
      <a href=https://github.com/lucklab/erplab/wiki/ERPLAB-Tutorial#tutorial-table-of-contents>
        <img src="https://github.com/lucklab/erplab/wiki/images/ionicicons/ios7-arrow-forward.png" alt="forward arrow" height="75">
        <br>
        Tutorial 2: ERP Plotting and Measuring
      </a>
    </td>
  </tr>
</table>