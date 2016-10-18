## Brief Description of the Example Experiment
The initial examples come from a published experiment.  In this section, we will provide a basic overview of the experiment, along with a few of the details you will need to know to analyze it.  For a complete description of the experimental paradigm, see the publication ([Luck et al., 2009, _Psychophysiology, 46:_ 776-786](http://mindbrain.ucdavis.edu/people/sjluck/pdfs/Luck%202009%20Psychophys%20Schizophrenia%20P3-LRP.pdf)).

This study examines the P3 wave and the lateralized readiness component (LRP) in a group of schizophrenia patients and a group of matched control subjects.  This tutorial focuses on the data from 6 of the control subjects (in the folders named S1 – S6; but note that some releases contain only the data from subject S1).  All subject identity information has been stripped from the data files.

In this experiment, a letter or digit was presented every 1300-1700 ms. Subjects were instructed to press a button with one hand for digits and with the other hand for letters.  For a given trial block, either the letters or the digits were rare (20%) and the other category was frequent (80%).  Thus, the stimulus category and the probability were counterbalanced.  The probability manipulation was designed to isolate the probability-sensitive P3b component. Different event codes were used for the digits when they were rare, the digits when they were frequent, the letters when they were rare, and the letters when they were frequent. (The experiment also included a condition in which the two categories were equiprobable, but that condition is not included in this tutorial.)

The experiment was also designed to isolate the LRP by counterbalancing the stimulus category and probability with the left and right hand responses.  That is, subjects responded to letters with the left hand and digits with the right hand for half of the experiment, and they responded to digits with the left hand and letters with the right hand for the other half.  This is also indicated by the event codes for each stimulus (i.e., the event code for the stimulus also indicates the appropriate response for that stimulus).

ERPLAB Toolbox makes no distinction between stimulus event codes and response event codes.  This gives the user more power, but it also gives the user responsibility for using the event codes in a sensible way. The event codes for responses in this example experiment indicated whether the response was correct (event code = 9) or incorrect (event code = 8) rather than directly indicating whether a left-hand or right-hand response was made.  However, the combination of the stimulus event code and the response event code makes it possible to determine whether the subject pressed the left button or the right button.

Here is a table showing the stimulus event codes.

    Event Code	  Category      Probability     Correct Response
    11	          Letter        Frequent        Left Hand
    21	          Digit         Rare            Right Hand
    112	          Letter        Rare            Left Hand
    122	          Digit         Frequent        Right Hand
    12	          Letter        Rare            Right Hand
    22	          Digit         Frequent        Left Hand
    111	          Letter        Frequent        Right Hand
    121	          Digit         Rare            Left Hand
 

The data in this experiment were recorded from a 16-bit Neuroscan Synamps system with a bandpass of 0.05-100 Hz and a sampling rate of 500 Hz.  Each scalp site was recorded relative to a right-earlobe reference.  Recordings were also obtained from a vertical electrooculogram (VEOG) electrode located beneath the left eye and from an electrode on the left earlobe (both referenced to the right earlobe).  A horizontal electrooculogram (HEOG) signal was recorded as the potential between electrodes located just lateral to each eye.

Letters and digits were presented in an unpredictable order within each trial block, but separate blocks were used for each combination of probability response assignment.  That is, there were separate trial blocks for: (1) 80% letters (left-hand response) and 20% digits (right-hand response); (2) 20% letters (left-hand response) and 80% digits (right-hand response); (3) 80% letters (right-hand response) and 20% digits (left-hand response); (4) 20% letters (right-hand response) and 80% digits (left-hand response).  Each block was originally recorded in a separate file. 

These files were imported into EEGLAB (using **File > Import data > From Neuroscant .CNT File**) and then merged together (with **File > Append datasets**).  The procedure you follow will depend on your data acquisition system.  Note that EEGLAB places a boundary event code at the boundary between the original files to mark the fact that a temporal discontinuity was present at those times.  This is important, because some functions (e.g., filters) either implicitly or explicitly assume that consecutive data points in the **EEG** reflect temporally consecutive moments in time (see the section on boundary events in the ERPLAB User's Manual).  The end result was saved in a file named S1_EEG.set (or S2, S3, etc., to indicate each individual subject).


<!--Bottom Navigation HTML-->
<br><br><br><br><br><br><br>
----
<table >
  <tr>
    <td  align="right" width="40%">
      <a href="./Getting-Started:-Tutorial">
        <img src="https://github.com/lucklab/erplab/wiki/images/ionicicons/ios7-arrow-back.png" alt="back arrow" height="75">
        <br>
        Getting Started
      </a>
    </td>
    <td  align="center" width="20%">
      <a href="./Tutorial">
        <img src="https://github.com/lucklab/erplab/wiki/images/ionicicons/ios7-copy.png" alt="tutorial icon" height="75">
        <br>
        Tutorial
       </a>
    </td>
    <td  align="left" width="40%">
      <a href="./Adding-Channel-Locations-to-your-Dataset:-Tutorial">
        <img src="https://github.com/lucklab/erplab/wiki/images/ionicicons/ios7-arrow-forward.png" alt="forward arrow" height="75">
        <br>
        Adding Channel Locations to your Dataset
      </a>
    </td>
  </tr>
</table>