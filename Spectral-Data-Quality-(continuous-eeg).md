ERPLAB now provides a Spectral Data Quality (continuous eeg) routine that can give you coarse information about the amount of power in different frequency bands . This can be useful for examining the frequencies that make up the EEG signal, and show if there are artifacts, like 50 / 60 Hz electrical line noise. 

**Note:**
* This routine only works with continuous EEG data
* This routine should be used after eliminating extreme periods of noise using [Artifact Rejection (continuous EEG)](https://github.com/lucklab/erplab/wiki/Artifact-Rejection-in-Continuous-Data), and after eliminating break periods using [Delete Time Segments (continuous EEG)](https://github.com/lucklab/erplab/wiki/Continuous-EEG-Preprocessing), otherwise the spectra will be contaminated with undue noise. 

Action:

`[EEG, fft_out] = pop_continuousDFT( EEG, 'ChannelIndex',  1:64, 'Frequencies', [ 0 3; 3 8; 8 12; 8 30; 30 48; 49 51; 59 61; 0 250], 'FrequencyLabel',...
 {'delta' 'theta' 'alpha' 'beta' 'gamma' '60hz-noise' '70hz-noise' 'broadband' }, 'PercentRandom',  20, 'viewGUI',...
 'true' );`

Result: 

This routine returns the averaged single-sided amplitude of frequency bands via Fast Fourier Transform from 5 second windowed segments of the continuous EEG. The windows are created and randomly selected from 20% of entire dataset to speed the routine performance. Using the GUI (see below), you can press "RESET" to use the default frequency bands that are commonly used in the neurosciences, or input new bands. In addition, you can select which channels to output spectral data from (you should not include channels that are not brain data, like eye-tracking channels or photodiodes). 

![Screen Shot 2023-02-10 at 6 20 02 PM](https://user-images.githubusercontent.com/45770852/218234071-3153471f-c0d9-4975-80a8-904eb6e7e326.png)

### Data Quality Metrics - Viewer & Spectral Plotting

![Screen Shot 2023-02-10 at 6 38 50 PM](https://user-images.githubusercontent.com/45770852/218235081-73460924-6d8c-4554-ada2-566fb230d0d7.png)


Using the Viewer, you are able to change between spectra information in Amplitude or Power, and the results can be exported to either a matlab data file or Excel. 

In order to plot spectral information, you must select **one** column in the data table as the frequency band, and as many channels/rows to represent the average across all the channels in that frequency band. **The selection is made by clicking on the data table with your mouse.**
After the selection is made, press "PLOT". 


![Screen Shot 2023-02-10 at 6 42 12 PM](https://user-images.githubusercontent.com/45770852/218234910-7e321c8b-4df8-424d-8548-4db3af152ae7.png)










