The **Spectral Data Quality (continuous eeg)** routine provides coarse information about the amount of power in different frequency bands. This is useful for assessing types of noise that are confined to specific EEG bands. For example, skin potentials predominantly produce low-frequency voltages (under ~3 Hz), and line noise produces narrow spikes at the line frequency (60 Hz in North America and some other parts of the world, 50 Hz in Europe and most of Asia). This routine allows you to quantify the amplitude or power in whatever frequency bands you like. More precise information about data quality can be obtained at the time of averaging with our [other data quality metrics](https://github.com/lucklab/erplab/wiki/ERPLAB-Data-Quality-Metrics). However, those metrics require more extensive preprocessing, and the **Spectral Data Quality (continuous eeg)** routine provides a quick assessment of data quality on the continuous EEG with minimal preprocessing. This routine works only with continuous EEG data.

**Important Notes:**
* Before using this routine, you should do a quick cleaning of the continuous EEG using both [Delete Time Segments (continuous EEG)](https://github.com/lucklab/erplab/wiki/Continuous-EEG-Preprocessing) and [Artifact Rejection (continuous EEG)](https://github.com/lucklab/erplab/wiki/Artifact-Rejection-in-Continuous-Data).
* These routines will eliminate the periods of time between trial blocks and periods with extreme noise (e.g., when an electrode has become disconnected or the subject scratches the electrode cap).
* These periods will not impact your final data quality, but they can have a large impact on the **Spectral Data Quality (continuous eeg)** routine. If you do not remove them, the output of this routine may be misleading.
* For a more sophisticated approach to characterizing EEG frequency content, see the [FOOOF package](https://fooof-tools.github.io/fooof/) from the Voytek lab.

## Running the routine from the GUI 

To run this routine from the GUI, select **ERPLAB > Preprocess EEG > Spectral Data Quality (continuous eeg)**. You will then see the window shown below. It allows you select a subset of channels for analysis. It also allows you to select which frequency bands to quantify. We provide a set of defaults, but you can edit and delete those bands, and you can add additional bands. The **Reset** button restores the defaults. Once you are satisfied with the parameters, click the **Run** button.

![Screen Shot 2023-02-10 at 6 20 02 PM](https://user-images.githubusercontent.com/45770852/218234071-3153471f-c0d9-4975-80a8-904eb6e7e326.png)

The routine will take some time to run (typically between 10 seconds and 2 minutes, depending on the size of the dataset and the speed of your computer). When it completes, it shows the results in a Viewer window, as shown in the screenshot below. The Viewer shows the amplitude or power for each band, separately for each channel. These values can be exported to either a Matlab data file or an Excel spreadsheet.

If you see a value of NaN in the Viewer, this usually means that the corresponding frequency band is not valid for the current dataset. In particular, the maximum frequency is 1/2 the sampling rate (e.g., 128 Hz if your sampling rate was 256 Hz).

This can be a lot of information, so we provide two options for highlighting extreme values. If you check the **Color heat map** box, each cell of the table will be color-coded according to the amplitude or power of that cell. If you check the **Outliers** button, any cells that are more than X standard deviations from the mean for that band will be highlighted. (The default for X is 2, but you can adjust this with the text box.)

![Screen Shot 2023-02-10 at 6 38 50 PM](https://user-images.githubusercontent.com/45770852/218235081-73460924-6d8c-4554-ada2-566fb230d0d7.png)

You can also plot the amplitude or power for each individual frequency within a selected band, as shown in the screenshot below. First, select one or more channels from a single frequency band. Then click the **Plot** button to see a graph of amplitude or power over the frequencies within that band (averaged over the selected channels).

![Screen Shot 2023-02-10 at 6 42 12 PM](https://user-images.githubusercontent.com/45770852/218234910-7e321c8b-4df8-424d-8548-4db3af152ae7.png)


## Details of the algorithm

This routine returns the averaged single-sided amplitude of frequency bands via Fast Fourier Transform from 5 second windowed segments of the continuous EEG. The windows are created and randomly selected from 20% of entire dataset to speed the routine performance. Using the GUI (see below), you can press "RESET" to use the default frequency bands that are commonly used in the neurosciences, or input new bands. In addition, you can select which channels to output spectral data from (you should not include channels that are not brain data, like eye-tracking channels or photodiodes). 


## Script equivalent

`[EEG, fft_out] = pop_continuousDFT( EEG, 'ChannelIndex',  1:64, 'Frequencies', [ 0 3; 3 8; 8 12; 8 30; 30 48; 49 51; 59 61; 0 250], 'FrequencyLabel',...
 {'delta' 'theta' 'alpha' 'beta' 'gamma' '60hz-noise' '70hz-noise' 'broadband' }, 'PercentRandom',  20, 'viewGUI',...
 'true' );`










