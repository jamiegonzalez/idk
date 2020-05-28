## Getting started
We assume that Matlab is installed, that EEGLAB is installed and in the Matlab path, and that ERPLAB is correctly installed in the EEGLAB plugin subfolder. If not, see the [installation instructions here](https://github.com/lucklab/erplab/wiki/Installation).

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

## Loading EEG data

Download the [example EEG data files here](https://ucdavis.box.com/shared/static/f1go6b880w82cle1l53pucvsymcbp4st.zip). Unzip to a known folder, here we show `C:\m\eegdata\erplab_tut`. Note that there is a subfolder for each experiment subject, S1 to S6.

![Tut_data_folder2](https://user-images.githubusercontent.com/5137405/83183516-c49b9000-a0dc-11ea-89d0-64834b883ade.png)

Within the `S1` subfolder, you the `S1_EEG.set` file. This file contains the continuous EEG data for subject 1 in EEGLAB format, and also includes some meta data, like the event code timing information.


