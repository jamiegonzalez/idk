Hello,

I am currently working on a project that incorporates the contralateral delay activity waveform. I am using EEGLAB v14.1.2 with MATLAB vR2011b. I had a few questions that arose throughout my final pipeline steps.

I first plot the waveforms for my ERPs and examine the channels of interest to ensure that the contralateral side of the hemifield event is more negative than the ipsilateral side of the hemifeild event. Next, I use the following equation in the ERP bin operations menu to conduct the initial calculations for the contralateral and ipsilateral waveforms: 

`prepareContraIpsi`
`Lch = [ 18 13 22 23 28]`
`Rch = [ 21 17 26 25 30]`
`nbin1 = 0.5*bin1@Rch + 0.5*bin2@Lch label Ipsi ND`
`nbin2 = 0.5*bin1@Lch + 0.5*bin2@Rch label Contra ND`
`nbin3 = 0.5*bin3@Rch + 0.5*bin4@Lch label Ipsi NT2`
`nbin4 = 0.5*bin3@Lch + 0.5*bin4@Rch label Contra NT2`
`nbin5 = 0.5*bin5@Rch + 0.5*bin6@Lch label Ipsi NT4`
`nbin6 = 0.5*bin5@Lch + 0.5*bin6@Rch label Contra NT4`

As you can see from the code, there are 3 conditions: NT2 (2 targets), NT4 (4 targets), and ND (2 targets and 2 distractors). After performing this contra-ipsi calculation, I go to view the waveforms of my channels of interest to again ensure that contralateral is more negative than ispilateral. However, during this stage I begin to notice a few errors/issues with some of the subjects' data. Specifically, one of the channels of interest now only shows the contralateral waveform for each of these conditions. To make this matter more complicated, this does not occur with all of my subjects. In addition, when it does happen to a few of my subjects, it is almost never the same channel that seems to be affected. I've gone back and examined the raw ERP waveforms, and these channels do not seem to be having any issues at this stage. 

**Does anyone have any idea what may be causing this, or if it is an issue with my equation? Or how to resolve this issue?**

After this stage, I go on to process the CDA for each of my channels of interest. I use the following code again through bin operations:

`nbin1 = bin1 - bin2 label Contra-Ipsi ND`
`nbin2 = bin3 - bin4 label Contra-Ipsi NT2`
`nbin3 = bin5 - bin6 label Contra-Ipsi NT4`

All of my channel waveforms show the expected CDA (e.g., greater negativity for NT4 than NT2), except for the channels that seemed to be missing their ipsilateral waveform from the step/issue I described prior. So again, it is imperative that I correct this prior issue first. 

**I also wanted to check to make sure that this second step is also correct in the pipeline for calculating CDA. Or is there a more accurate way to do this?**

Finally, I take the average of my channels of interest and examine each individual subjects CDA. Then, I create the grand average waveform across all subjects. 

**Is processing through each individual subject's CDA and then grand averaging the correct procedure for calculating CDA? Or should I instead create a grand average of all subjects raw ERPs, and begin the CDA computations with that grand average ERP?**

I apologize for the lengthy post. Any assistance here is greatly appreciated. Thanks!


