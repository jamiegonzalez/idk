## ERP Bin Operations
**ERPLAB > ERP Operations > ERP Bin Operations** allows you to compute new bins that are combinations of the bins in the current ERP structure.  For example, you can average multiple bins together, and you can compute difference waves.  To use it, you will write simple equations that describe how the new bin is computed.  For example, to create a new Bin 3 that is the average of the current Bin 1 and Bin 2, you would write the following equation: "b3 = (b1+b2)/2" (or "b3 = 0.5*b1 + 0.5*b2").  The screenshot below shows the GUI.  You will usually want to create a label for a new bin by putting "label _something_" at the end of the equation.  In the example below, a difference wave is being created (b3 = b2 – b1) and "Rare minus Frequent difference wave" is specified as the label.

bin_operations_gui

 

The panel at the right side of the Bin Operations GUI lists the bins in the current ERPset.  The panel at the left side of the window contains the equations for creating the new bins.  The equations can be saved in a file (using **Save list** or **Save list as**) and loaded again at a later time (using **Load list**).  When you click **RUN**, the equations are sent to the routine that performs the requested computations.  Ordinarily, the equations in the window are sent as a set of strings (a cell array).  With a long list of equations, this will lead to a very complicated function call in your history.  If you check **Send file rather than individual equations**, the file will be sent instead of the equations, making the history simpler (which is convenient if you plan to turn the history into a script).  But the same bin operations will be performed either way.

Basically any standard mathematical equation can be used.  Here are some examples:

B5 = ((b1+b2)/2) – ((b3+b4)/2) label Average of bins 1 and 2 minus average of bins 3 and 4

Bin5 = sqrt(b2^2 + b3^2) label Square root of sum of squared bins 2 and 3

b5 = abs(b4) label Absolute value of bin 4 (rectification)

bin5 = b4 + 1 label Add an offset of 1 microvolt to the bin 4 waveform

                 

In addition, we have defined a function that averages together a set of bins, weighted by the number of epochs that contributed to each bin (which is stored in the **ERP** structure).   For example, if 10 epochs were originally averaged together into bin 1 and 90 epochs were originally averaged together into bin 2, you could create a bin that is equivalent to what you would have gotten by averaging these 100 epochs together during the initial averaging process (which is the same as "(10*bin1 + 90*bin2)/100").  It is used as follows:

Bin3 = wavgbin(1, 2) label Weighted average of bins 1 and 2

Bin9 = wavgbin(1:8) label Weighted average of bins 1 through 8

Bin20 = wavgbin(1:4,6,9,12:15) label Weighted average of bins 1-4, 6, 9, and 12-15

                 

## Modes of Operation
Bin Operations has two modes of operation, which are selected with the two buttons at the bottom right of the GUI (see screenshot above).  In one mode, the equations modify existing bins and add new bins within the current ERPset.  In this mode, you can modify one bin and then use this modified bin to create or modify another bin (this is called _recursive updating_).  In another mode, the current ERPset serves as the input to equations, and a new set of bins is created in a new ERPset (this is called performing a set of _independent transformations_).  The ERPLAB Tutorial provides detailed examples of these two modes.

Creating a new ERPset.  When you are creating a new ERPset, your equations begin with "nb" or "newbin" as a reminder that you are creating a new bin within a new ERPset.  You must start with bin 1 ("nb1 =" or "newbin1 =") and then continue consecutively with bins 2, 3, 4, etc.  You can have as many or as few bins in the new ERPset as you desire in this mode.  Consider this example, in which the current ERPset contains 4 bins:

nb1 = b4

nb2 = b1

In this example, the bin 1 in the new ERPset is simply bin 4 from the current ERPset, and bin 2 in the new ERPset is simply bin 1 from the current ERPset.  Thus, the new ERPset contains only two bins, and they are in a different order than in the original ERPset.

Modifying the current ERPset.  When you are modifying the current ERPset, bins are referenced as "b" or "bin" on both sides of the equals sign (e.g, "b3 = b2 – b1" or "bin3 = bin2 – bin1").  In this mode, you can modify existing bins or add new bins, but you cannot delete bins.  If you try to reorder the bins, you will likely run into problems.  Consider the following example, which looks as if it should swap the order of bins 1 and 2:

b1 = b2

b2 = b1

If you were to try this when modifying an existing ERPset, the first line would cause the contents of bin 1 to be replaced with the contents of bin 2.  The second line would then cause bin 2 to be replaced with this newly updated version of bin 1 (which now holds the original data from bin 2).  Thus, you would end up with the original contents of bin 2 in both bin 1 and bin 2.

Despite this limitation, it is often more convenient to modify the existing ERPset than to create a new ERPset.  For example, this mode allows you to add a set of difference waves to the end of the current ERPset rather than having two ERPsets, one for the original data and one for the difference waves.  In addition, it can sometimes be efficient to create a bin and then use this new bin in equations that create additional bins.

_Hint: When you are modifying an existing ERPset, you might first want to make a duplicate of the current ERPset and work on that duplicate, as described in the [section on saving ERPsets](https://github.com/lucklab/erplab/wiki/Saving,-Loading,-Duplicating,-Renaming,-Clearing,-and-Exporting-ERPSETS)._

When you are modifying an existing ERPset, your list of equations does not need to re-define the existing bins.  However, the bins that are defined must be in ascending order, and the result cannot have any missing bins.  For example, if the current ERPset contains bins 1-10, you could have a list of equations like this:

B3 = B1 – B2 label Re-definition of bin 3

B11 = B3 – B5 label Create new bin 11 as difference between bin 5 and newly updated bin 3

B12 = B11^2 label Create new bin 12 that is the new bin 11 squared

However, you could not have a list of equations that began with bin 12 (because bin 11 has not yet been defined) or a list in which bin 12 came before bin 11.

## Specifying subsets of channels (especially to compute contra versus ipsi)
It is also possible to specify different subsets of channels for the different bins being used in a given equation, which is especially useful for isolating the N2pc and LRP components.  For example, if you are trying to compute a lateralized readiness potential (LRP) waveform, you will want to subtract trials with an ipsilateral response from trials with a contralateral response, averaged across the left and right hemispheres.  That is, you want to make a contralateral average (left-hemisphere electrode sites for right-hand responses averaged with right-hemisphere electrode sites for left-hand responses) and an ipsilateral average (left-hemisphere sites for left-hand responses averaged with right-hemisphere sites for right-hand response) and compute the difference. This section will describe how to do this manually.  The next section will describe the contra/ipsi assistant, which can do much of the work for you.

To do this in Bin Operations, you first define sets of electrodes corresponding to the left and right hemispheres.  Imagine that the electrode sites 1-6 are as follows 1=F3, 2=F4, 3=C3, 4=C4, 5=P3, 6=P4.  And imagine that Bin 1 corresponds to left-hand responses whereas Bin 2 corresponds to right-hand responses.  The following shows how you would define left- and right-hemisphere groups and use them to form a contralateral waveform (new Bin 1), an ipsilateral waveform (new Bin 2), and a contra-minus-ipsi difference wave (new Bin 3):

LH = [1 3 5]

RH = [2 4 6]

b1 = (b2@LH + b1@RH)/2 label Average Contra

b2 = (b1@LH + b2@RH/2 label Average Ipsi

b3 = ((b2@LH + b1@RH)/2) – ((b1@LH + b2@RH)/2) label Average Contra Minus Ipsi

In this example, we first define two electrode groups, named LH and RH (containing the left-hemisphere and right-hemisphere electrode sites, respectively).  We then specify which electrode groups should be used for each bin by connecting the bin number and the electrode group with @ symbol.

The resulting ERPset would have only 3 channels (automatically labeled 'F3/4' 'C3/4' 'P3/4').  Because the new bins have fewer channels than the old bins, you would not be able to update the existing ERPset when creating these new bins; you would need to create a new ERPset.

You can have ERPLAB automatically create left- and right-hemisphere groups on the basis of the channel labels.  Specifically, the "LH =" and "RH =" lines in the above example could be replaced by the following line:

[LH RH] = splitbrain(ERP)

The **splitbrain()** function finds pairs of electrodes whose names are identical except for ending with consecutive odd (for left-hemisphere) and even (for right-hemisphere) numbers (following the International 10/20 System convention).  For example, it would treat Fp1 and Fp2 as corresponding left-right pairs.  But the electrode names do not have to be standard 10/20 names (e.g., it would treat Temporal125 and Temporal126 as corresponding left-right pairs).  Any electrode sites that don't end in a number will be excluded from the channel groups (e.g., Fz), and will generate a warning (which you can usually ignore because you usually want to exclude such electrodes when creating left-right pairs).

Note that, although "LH" and "RH" were used to name the electrode groups in these examples, you can use any strings to name the groups. Also, this can be used to create any kind of channel subsets that you'd like, not just left hemisphere and right hemisphere subsets.

## Using the Contra/Ipsi Assistant
The ERP Bin Operations GUI contains a button labeled **contra/ipsi assistant**.  This button brings up the GUI shown below, which will create the equations for making the contra and ipsi waveforms (for most experiments).

contra_ipsi_assistant

The first two text boxes are used to list the left- and right-hemisphere channel pairs.  You need to make sure that the channels are in the same order for both the left and right sides (e.g., channels F3, C3, and P3 [in that order] for the left side and F4, C4, and P4 [in that order] for the right side).  If you click the **auto** button, ERPLAB will attempt to find the appropriate channels for you (on the basis of standard naming conventions).

You then need to specify which bins correspond to trials on which attention will be directed to the left versus right hemifields.  For example, imagine that you have the following bins:

Bin 1: Red target in the left visual field

Bin 2: Red target in the right visual field

Bin 3: Blue target in the left visual field

Bin 4: Blue target in the right visual field

Bins 1 and 3 would go into the left hemifield text box, and bins 2 and 4 would go into the right hemifield text box.

Bins 1 and 2 will then be converted into a contra bin and an ipsi bin for the red targets, and Bins 3 and 4 will then be converted into a contra bin and an ipso bin for the blue targets.  You would provide labels for these new bins (e.g., red_targets for the new bins 1 and 2, and blue_targets for the new bins 3 and 4).

Once you click **OK**, you will get a set of equations like this:

prepareContraIpsi                                              

Lch = [ 1 7 3 5 8]                                             

Rch = [ 2 10 4 6 9]                                            

nbin1 = 0.5*bin1@Rch + 0.5*bin2@Lch label red_targets Contra   

nbin2 = 0.5*bin1@Lch + 0.5*bin2@Rch label red_targets Ipsi     

nbin3 = 0.5*bin3@Rch + 0.5*bin4@Lch label blue_targets Contra  

nbin4 = 0.5*bin3@Lch + 0.5*bin4@Rch label blue_targets Ipsi    

# For creating contra-minus-ipsi waveforms from the bins above,

# run (only) the formulas described here below in a second call

# of "ERP binoperator"  (remove the # symbol before run them)  

#bin5 = bin1 - bin2 label red_targets  Contra-Ipsi             

#bin6 = bin3 - bin4 label blue_targets  Contra-Ipsi            

You then run ERP Bin Operations (using Independent Transformations mode) to create the new bins.  The equations include comments telling you how you can create contra-minus-ipsi difference waves, but this must be done in a second step, after the contra and ipsi bins have been made (i.e., you will need to run ERP Bin Operations a second time with these new equations to make the difference waves).