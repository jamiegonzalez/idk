## Averaging ERPs
Computing averaged ERPs from an epoched dataset is quite simple.  There is only one slight complication, which is that it is possible to average across multiple sets of EEG data at one time.  Imagine, for example, that you recorded half of the data for a given subject on one day and the other half on a different day, resulting in two separate EEG files (stored in separate datasets).  Or imagine that you have 6 conditions, and each was recorded in a separate file.  You could average each of the datasets separately and then combine the averages using **ERPLAB > Average Across ERPsets**.  However, ERPLAB makes it possible to combine them during the averaging process, which is usually easier.  This is accomplished by simply specifying multiple datasets when you average.  All the datasets are then treated as if they are one big dataset (this is sometimes called "weighted averaging", because each trial is weighted equally).

To compute averaged ERPs, you must first load one or more epoched datasets in EEGLAB.  You can then select **ERPLAB > Compute Averaged ERPs**. In the window that appears, enter the # of the dataset that contains the data you would like to average (or multiple datasets). For example, if you want to average the epochs in dataset #2, you would simply type '2' into the window.  If you wanted to average the epochs in datasets 2, 3, and 5, you would type '2 3 5' into the window.  Or, if the datasets are consecutive, you could type something like '1:3' into the window (as in the screenshot below). The current dataset is the default. If you aren't sure what the number of your dataset is, just look in the **Datasets** menu. Click **RUN** to compute the averaged ERPs.

![ERPLAB_v8_AVG](https://user-images.githubusercontent.com/5137405/78292016-3db2a880-74db-11ea-9d5c-183cde9a9257.png)

 You will ordinarily want to exclude all epochs that have been marked as containing artifacts. It is also possible to ignore the artifact marks by selecting **Include ALL epochs**.  You can even include only the epochs with artifacts (by selecting **Include ONLY epochs marked with artifact rejection**), which could be helpful in seeing exactly how the artifacts are distorting the data.

There is also a box that allows you to exclude trials in which a boundary event code or an invalid event code (i.e., one in which the enable flag is set to zero) is present within the EEG epoch. These should be rare occurrences, but you will almost certainly want to exclude such epochs if they are present.

_Important note: Although ERPLAB keeps track of artifacts using the artifact flags in the **EEG.EVENTLIST** structure, EEGLAB instead uses the **EEG.reject** structure.  When ERPLAB detects an artifact, it updates both **EEG.EVENTLIST** and **EEG.reject**.  When EEGLAB's artifact detection routines are used, only **EEG.reject** is updated.  Consequently, ERPLAB checks to make sure that **EEG.EVENTLIST** and **EEG.reject** have the same artifact marks, producing a warning message if they differ.  If they differ, you can synchronize the information in **EEG.EVENTLIST** and **EEG.reject** with the **ERPLAB > Artifact Detection > Synchronize Artifact Info in EEG and EVENTLIST** command._





## Data Quality measures
During the averaging process, ERPLAB can compute several measures of data quality. This is done automatically by default (although you can disable it by selecting No Data Quality measures in the Data Quality Quantification section of the averaging window). For a big-picture overview of how ERPLAB computes and stores data quality measures, see the [overview of data quality](https://github.com/lucklab/erplab/wiki/ERPLAB-Data-Quality-Metrics).

By default, ERPLAB will compute:

1. **Baseline Noise** - the noise level of the baseline period (the standard error of the voltage during the period prior to time zero) for each waveform.

2. **Point-wise SEM** - the standard error of the mean at each time point for each waveform.

3. **aSME** - the analytic standardized measurement error (aSME) for each waveform using a set of default time windows.

The SME quantifies the standard error of measurement for the mean voltage during a specific time window. 
You can change the time windows by selecting On- custom parameters and clicking the Set DQ options… button. The most common modification is to select one or more SME time windows that correspond to the time windows that you will use to measure the mean amplitudes of the ERP components. See the next subsection for more information about customizing the data quality measures. 

We encourage you to report the SME values in publications so that readers can assess the quality of your data. You can aggregate the SME values across participants when you make a grand average. If you report the SME values in your publications, please cite this paper:

Luck, S. J., Stewart, A. X., Simmons, A. M., & Rhemtulla, M. (2021). Standardized measurement error: A universal metric of data quality for averaged event-related potentials. Psychophysiology, 58, e13793. [https://doi.org/10.1111/psyp.13793](https://doi.org/10.1111/psyp.13793)


When averaging is complete, the lowest, highest, and median SME values (from among every combination of channel, bin, and time window) will be printed to the command window. All the SME values, along with the baseline noise measures, are stored in the Matlab workspace as ERP.dataquality. Options for display the values in the command window or saving them to a file can be found in ERPLAB > Data Quality Options. The standard error of the mean for each time point is stored in ERP.binerror and can be plotted using ERPLAB >  Plot ERP > Plot ERP Waveforms

### Default and custom setting of data quality parameters and time windows
By default, aSME is computed in a number of 100 ms windows, which are centered around 0 ms in the ERP epoch. The number and time range of the aSME windows, along with other data quality parameters, can be customized at the point of the ERP Averager. 

### Compute analytic standard deviation (aSD)
This provides a measure of data quality that does not directly depend on the number of trials (whereas the SME factors in the number of trials being averaged together). The mean amplitude across a given time range is measured on each trial, and the SD of these values across trials is computed.

### Compute pointwise standard error of the mean (SEM)
You can also choose to compute the standard error of the mean (across all epochs, separately for each time point in each bin) along with the average. This standard error data will be saved in the ERP.binerror matrix, and so be saved with your ERPset. This can later be plotted with your ERP. Note that the standard error is removed by certain other processing steps (e.g., filtering, bin operations, averaging across ERPsets) because these steps render the previous standard error meaningless.


### Correcting for bias
Analytic SD, SEM, and SME estimates exhibit a bias that varies with the number of trials: As the number of trials gets smaller, these estimates become progressively lower than the true value. We provide an option that corrects for this bias (Gurland & Tripathi, 1971). We recommend using this option, but it is off by default (to maintain backward compatibility with previous versions of ERPLAB that did not include this option). Unfortunately, we know of no simple correction that can be applied to bootstrapped values.




## Saving the new averaged ERP
When the averaged ERPs have been computed, a window will appear allowing you to name and save the ERPset containing the new **ERP** structure (see screenshot below).  This same window appears whenever you create a new ERPset.  Here's how it works:

* You can choose to either overwrite the current ERPset or create a new ERPset.  ERPsets don't usually take up much RAM, so you will almost always want to create a new ERPset.

* You need to choose a name for the ERPset.  This will be the name shown in the **ERPsets** menu.

* You can optionally save the ERPset as a file.  If you click the **same as erpname** button, it will give the file the same name as the ERPset (recommended in most cases), but with a **.erp** extension.  By default, it will be saved in the current folder.  However, you can use the **Browse** button to browse through your file system to find a place for it (or you can include the path explicitly along with the filename).

![ERP_avg_save_gui](https://user-images.githubusercontent.com/5137405/78292647-39d35600-74dc-11ea-88bc-a9e422791310.png)

_Note: The averaging routine can average together multiple datasets, which is very useful when a single subject's data are divided into different datasets.  In principle, this routine can also average together the data from different subjects.  However, we recommend against this.  Instead, the data from each subject should be averaged individually, and then the **ERPLAB > Average Across ERPsets** should be used to average together these averages._