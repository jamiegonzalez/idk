## Getting started
We assume that Matlab is installed, that EEGLAB is installed and in the Matlab path, and that ERPLAB is correctly installed in the EEGLAB plugin subfolder. If not, see the [installation instructions here](https://github.com/lucklab/erplab/wiki/Installation).

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
There are several aspects to the EEG datasets that are good to keep in mind:

* What data do I have? How many EEG channels? What is the duration of the recording?

This can be found within the blue EEGLAB GUI (as shown in screenshots above), where the channels per frame tells you the number of channels. The number of epochs is 1, the epoch start time is 0, and the epoch end time is 2139 s, indicating that the loaded and currently selected EEG set is continuous data, and runs from t=0 s to t=2139 s, giving (2139/60) around a 35 minute recording. This is EEG data recorded at a sample rate of 500 Hz, so there are (2139 * 500) around 1,069,500 datapoints for each electrode. It is good practice to verify that this corresponds to the properties of the experimental data you load at this stage.

This information can also be accessed programatically within Matlab, with commands like: 
`EEG.nbchan` `size(EEG.data)` `EEG.srate`


* What events occur within this recording? Are there event codes (aka event markers, triggers) indicating the relevant times of stimuli presentation and response?
* What ERPs are desired? What timeframe is desired to show these ERPs?

