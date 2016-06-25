## The EVENTLIST Structure
This section describes the EVENTLIST structure, which lies at the core of ERPLAB. First, we would like to provide an overview of the processes leading up to averaging to help you see the big picture.  The basic steps are as follows:

- Extract a list of the event codes from the EEG data in a dataset and store it in an **EVENTLIST** structure.  This list may then be edited to add, delete, and/or modify the events (e.g., to add responses from your stimulus presentation system, to add eye movement onsets from an eye tracker, to delete spurious event codes, etc.).  The [next section of the documentation](https://github.com/lucklab/erplab/wiki/Creating-An-EVENTLIST) provides details of creating an eventlist.
- You can also export the Eventlist to a text file, edit it, and import it back into the EEG dataset or into an ERPset ([see documentation here](https://github.com/lucklab/erplab/wiki/Exporting,-Editing,-and-Importing-EVENTLISTS)).
- Using the events stored in the **EVENTLIST** structure, determine which events will be assigned to each bin.  This is usually accomplished with the [BINLISTER](https://github.com/lucklab/erplab/wiki/Assigning-Events-to-Bins-with-BINLISTER) routine.
- [Convert the continuous EEG](https://github.com/lucklab/erplab/wiki/Epoching-Bins) in the dataset into a set of fixed-duration epochs, time-locked to the relevant events in the **EVENTLIST** structure.
- Apply [artifact detection](https://github.com/lucklab/erplab/wiki/Artifact-Detection-in-Epoched-Data) routines to mark epochs that should be excluded from averaging.  The epochs are not deleted; they are simply marked in the **EVENTLIST** and then excluded from averaging in the next stage.
- [Average](https://github.com/lucklab/erplab/wiki/Computing-Averaged-ERPs) together the epochs for each bin, creating an **ERP** structure (which is stored in an ERPset).
- Perform [behavioral analyses](https://github.com/lucklab/erplab/wiki/Behavioral-Analyses) on the data stored in the **EVENTLIST**, possibly excluding events with artifacts so that the behavioral analyses reflect the same trials as the ERP waveforms.
Other processes may be interposed between these steps.  For example, one could filter the data after epoching but before artifact rejection.  However, these steps are usually conducted in this order without any interposed operations.

ERPLAB provides a great deal of power and flexibility in these steps.  To harness this power, you really need to understand the **EVENTLIST** structure.  You may be tempted to just skim this section; if you do, be sure to come back later to read this information carefully.  In the long run, you will save time (and aggravation!) by understanding the underlying logic and details of how ERPLAB works.

## What is the EVENTLIST for?
Sophisticated ERP experiments often involve complex sequences of events (stimuli, responses, EMG bursts, eye movements), and the event information stored by EEGLAB in the **EEG** structure is insufficient (or too difficult to access) for the analysis of many ERP experiments.  ERPLAB has thus created the **EVENTLIST** structure to allow this information to be stored and manipulated in a convenient manner. 

For each event, the **EVENTLIST** has a record indicating the event code, its time of occurrence, its duration, a set of 8 binary _artifact flags_ that indicate whether an artifact was present for that event (and the nature of the artifact), and a set of 8 binary _user flags_ that can be used to code anything that the user would like to represent about an event (e.g., whether the subject was in a state of high alpha, what task the subject was performing at the time of the event, etc.). It can be very convenient to have this information stored separately from the EEG data (e.g., for behavioral analyses), and the **EVENTLIST** structure can be saved as a text file as well as being appended onto the relevant EEG structure (which allows it to be saved and loaded along with the EEG structure). It is created from the current **EEG** structure. If you save the **EVENTLIST** as a text file, you can edit it with Matlab's text editor (or a program created in Matlab or some other language) and then reload it, causing it to overwrite the original set of events in the dataset.  This provides a mechanism for adding, deleting, and modifying events. 

_Note for ERPSS users: There is no "condition code" concept in ERPLAB, but user flags within the EVENTLIST can be used to emulate this concept._

The **EVENTLIST** contains a copy of all the event information stored in the **type** field of the **EEG** structure, plus information about events that have been marked for artifact rejection in the **reject** field of the **EEG** structure, along with several additional pieces of information that will be described later.  It is important to realize that EEGLAB doesn't "know" anything about the **EVENTLIST** structure.  Consequently, a little bit effort is sometimes needed to make sure that any changes you make to the **EVENTLIST** structure get copied back into the **EEG.event** and **EEG.reject** structure and any changes you make to these parts of the **EEG** structure get copies back into the **EVENTLIST** structure.  Any ERPLAB routines that modify the event codes in the **EVENTLIST** structure will ask you if you want to copy the modified events back into the **EEG.event** structure.  You can also do this manually with the **ERPLAB > Transfer eventinfo to EEG.type command**.  Similarly, when the **ERPLAB > Artifact Detection** routines are used to find artifacts, the **EEG.reject** structure will automatically be updated. The artifact information in **EEG.reject** and in the **EVENTLIST** structure can also be synchronized manually with [ERPLAB > Artifact Detection in Epoched Data > Synchronize Artifact Info in EEG and EVENTLIST](https://github.com/lucklab/erplab/wiki/Artifact-Detection-in-Epoched-Data) command. This manual synchronization is required when EEGLAB is used to reject or unreject epochs by visual inspection.

One key limitation of the **EEG.event** structure is that each event can be identified by a numeric event code or a text label, but you cannot have both.  ERPLAB allows you to have both in the **EVENTLIST** structure.  That way you can assign a text label for each numeric event code without losing the original numeric event codes (and vice versa).

Eventually you will convert your continuous EEG data into a set of  discrete epochs, time-locked to the events in the **EEG** structure (see the section on [epoching](https://github.com/lucklab/erplab/wiki/Epoching-Bins)).  When you do this, many of the events from the continuous EEG will not be time-locking events (e.g., response event codes will not be used as time-locking events if you are time-locking to stimulus events).  However, the **EVENTLIST** structure will continue to maintain all of the events.  This is important because artifact detection is performed on the epoched data, and you may want to exclude trials with artifacts from your behavioral analyses.  The **EVENTLIST** structure makes this possible because it contains all of the information about your stimuli and responses and can also contain information about which events were rejected because of artifacts.  The **EVENTLIST** structure does this by including both the original position of every event code plus the position of the time-locking events after the EEG data has been epoched.

## The Contents of an EVENTLIST
To understand the contents of an EventList, it is easiest to consider what the EventList looks like when saved to a text file.  Here is an example of a text-file version of an **EVENTLIST**, showing the first six events in a simple oddball experiment.

bin 1,         # 252,            Standard (correct)                                                                                 

bin 2,         # 63,             Target (correct)       

                                                                           

#item	bepoch	ecode	label 	        onset 	diff	dura	b_flags	a_flags	enable	bin
#				        (sec)	(sec)	(msec)	(binary)(binary)		
1	0	122	standard	8	0	0	0	0	1	[ 1 ]
2	0	9	std_resp	8.3962	0.3962	0	0	0	1	[    ]
3	0	122	standard	10	1.6038	0	0	0	1	[ 1 ]
4	0	9	std_resp	10.4265	0.4265	0	0	0	1	[    ]
5	0	132	target	12	1.5735	0	0	0	1	[ 2 ]
6	0	9	targ_resp	12.5191	0.519	0	0	0	1	[    ]
 

The file begins with a header (described later and not shown here) that indicates the name of the dataset from which the EventList was created, the sampling rate, the number of events, etc.  The next section of the file lists the bins for the file (we will say more about where this information comes from in a later section), along with the number of occurrences of each bin in the file (e.g., "# 252" means that there were 252 occurrences of this bin).

The next two lines are comments (any line beginning with a "#" is a comment); these comments are labels for the columns that follow.

Each of the following lines represents the information from an event, in order of occurrence.  The first column is the item number.   This number is not stored in the EVENTLIST structure, but is simply the position of the event within the EVENTLIST. 

The next column shows the epoch number (labeled 'bepoch' to indicate that this is based on ERPLAB's bin-based epoching routine, not EEGLAB's separate epoching routine).  In a continuous dataset, the epoch number is always listed as 0.  Once a datafile has been epoched, only a subset of the event codes remain in the datafile, but all of the events are retained in the EVENTLIST (e.g., response event codes may no longer be present after epoching).  To be able to determine which epoch in the datafile corresponds to a given event in the EVENTLIST, the EVENTLIST stores the epoch number of the event.  More precisely, the bepoch number in the EVENTLIST indicates the epoch within the epoched datafile for which the current event was the time-locking event.  Any events in the EVENTLIST that are not time-locking events within the epoched datafile have a bepoch value of 0.

The next two columns are the event code and label for the event.  Each event must have at least one of these two values to indicate what kind of event it was.  Labels are easier to remember than numbers, and we encourage you to use them.  Some EEG acquisition programs provide labels, but most provide only numeric codes.  ERPLAB provides a simple function that can add labels based on the numeric codes. Note that ERPLAB currently requires numeric values for any events that will be used to sort trials into bins for averaging.

The next three columns provide timing information.  The onset time is the most important column, because it indicates when the event code began (relative to the beginning of the file).  The "diff" column indicates the amount of time between the current event and the previous event; it is there for your information only (i.e., changing this value will not change the time of the event).  The "dura" column provides the duration of the event.  Some EEG acquisition systems provide real information about an event's duration (e.g., how long a button was held down).  ERPLAB does not currently use this information, but it is available for future expansion (and can be accessed by custom Matlab scripts).

The next column is a set of 8 binary _user flags_, each of which can have a value of 0 or 1.  These can be used for any purpose, but they are most commonly used to keep track of information used when the events are sorted into bins.  For example, if you have two conditions (e.g., attend red and attend green), you could use the user flags to indicate what task the subject was doing at the time of each event. You can set these values manually, with a script, or with the [BINLISTER](https://github.com/lucklab/erplab/wiki/Assigning-Events-to-Bins-with-BINLISTER) routine.

The user flags are followed by a set of artifact flags.  The rightmost of these (flag 1) indicates whether ERPLAB has detected an artifact for that event, and the others (flags 2-8) can be used to indicate what kind of artifact was detected.

Note: The artifact flags are set by ERPLAB's artifact detection routines.  These routines will also set values in **EEG.reject** so that rejected epochs are displayed in a special color by EEGLAB's plotting routines.  EEGLAB has additional artifact detection routines, and it also allows you to manually mark or unmark epochs for rejection.  However, this does not automatically set the appropriate flags in the EventList structure (because EEGLAB doesn't "know" anything about the EventList structure).  Also, if you manually change the artifact flags in the EventList structure (e.g., with a script or by editing a text version of the EventList structure), these changes will not be automatically propagated to **EEG.reject**.  In these cases, you can synchronize the information in the EventList flags and in EEG.reject with [ERPLAB > Artifact Detection in Epoched Data > Synchronize Artifact Info in EEG and EVENTLIST](https://github.com/lucklab/erplab/wiki/Artifact-Detection-in-Epoched-Data).  In addition, when you create averaged ERPs using **ERPLAB > Compute Averaged ERPs**, ERPLAB will automatically check for any differences between the EventList flags and **EEG.reject**; if it detects any differences, it will give you the opportunity to synchronize before averaging.

_Note for programmers: The artifact flags and user flags are stored together in a single integer variable, with the least significant byte being used for the artifact flags and the most significant byte being used for the user flags._

The next column is an "enable" value, which is used to indicate whether the event should be used or ignored by any routines that operate on the **EVENTLIST** structure.  For example, if the subject was asleep or an electrode was disconnected for a period of 20 events, this value could be set to zero for those events, and those events would be ignored during averaging. The same effect could be obtained by simply deleting the events from the **EVENTLIST**, but using the enable flag allows the events to be "turned back on" at a later point if desired. 

The final column is a "bin" field, which is used to determine which bin the event will be assigned to during the averaging process. In a simple oddball experiment, for example, Bin 1 might be the standard stimuli and Bin 2 might be the target stimuli. The bin assignment can be accomplished [when the EventList is first created](https://github.com/lucklab/erplab/wiki/Creating-An-EVENTLIST), or it can be accomplished using the [BINLISTER](https://github.com/lucklab/erplab/wiki/Assigning-Events-to-Bins-with-BINLISTER) routine.  Note that a given event might not be assigned to any bin (as in the response events in the example shown above).  In addition, a given event can be assigned to more than one bin (e.g., a target event could be assigned into a "Correctly Detected Targets" bin and also into an "All Targets" bin).

The header section of an EventList text file looks like this:

#  Non-editable header begin --------------------------------------------------------------------------------

#

#  data format...............: continuous

#  setname...................: S1_Chan_elist

#  filename..................: none_specified

#  filepath..................: none_specified

#  nchan.....................: 16

#  pnts......................: 1069520

#  srate.....................: 500

#  nevents...................: 2557

#  generated by (bdf)........:

#  generated by (set)........: S1_Chan_elist

#  reported in ..............:

#  prog Version..............: 1.1.721

#  creation date.............: 18-Jan-2010 07:43:40

#  user Account..............:

#

#  Non-editable header end --------------------------------------------------------------------------------

 

The following information is provided:

- ** The type of dataset: continuous or epoched
The name of the dataset from which the EventList was created
The name of the dataset that was created along with the EventList (if any)
The location of your saved dataset, if you chose to save your dataset
The number of channels in your dataset
The number of data points in your dataset
The sampling rate at which your data was recorded
The number of recorded event codes in your dataset
The name of the bin descriptor file (if any)
The version of ERPLAB that was used to create the EventList
The date that the EventList file was created
The user account of the person who created the file (if available)
 
Note that the header in the text file is not editable.  That is, the header is ignored when you import it back into ERPLAB, so any changes you make to it will have no effect.

You can also view the contents of an EVENTLIST structure directly from the Matlab command line by typing EEG.EVENTLIST.  Here's an example:

>> EEG.EVENTLIST
 
ans =
 
         setname: 'S1_Chan_elist'
          report: ''
         bdfname: [1x104 char]
            nbin: 2
         version: '1.1.725'
         account: 'luck'
        username: ''
    trialsperbin: [1009 242]
          elname: [1x145 char]
             bdf: [1x2 struct]
          eldate: '24-Jan-2010 15:59:00'
       eventinfo: [1x2557 struct]
 
The information about the individual events is in EEG.EVENTLIST.eventinfo, which is an array of sub-structures (one per event).  The fields in EEG.EVENTLIST.eventinfo are as shown in the example below.  Each of the fields in the text file has an obvious analog in the structure, except that the spoint field in the structure is not found in the text file.  This field stores the sample point number (i.e., how many sample points have occurred since the beginning of the file).  The time of the sample is computed from this value, in conjunction with the sampling rate (which is stored in EEG.EVENTLIST.info.srate).  The bini (bin index) field is an array of the bins to which the event has been assigned (if any).  As described above, the item field indicates the item number of the event within the EVENTLIST (event #1, event #2, etc.), and the epoch field indicates the epoch number of the event within the datafile (when the event is the time-locking event within an epoch).

ans =
 
1x2557 struct array with fields:
    item
    code
    binlabel
    codelabel
    time
    spoint
    dura
    flag
    enable
    bini
 

The EEG.EVENTLIST structure also contains several pieces of information that are filled by the BINLISTER routine, including the name of the bin descriptor file (stored in bdfname) and a list of the actual bin descriptors (stored in bdf).  This can help you figure out how a file was created when you come back to it at a later time.  The bdf field also contains reaction time information, when extracted by BINLISTER.