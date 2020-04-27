## ERPLAB v8.0 Release Notes

With ERPLAB v8.0, we include new tools for [assessing measures of Data Quality Metrics in EEG ERP data](https://github.com/lucklab/erplab/wiki/ERPLAB-Data-Quality-Metrics).

### Data Quality Metrics
- The ERP Averager will calculate these Data Quality Metrics by default
- A new submenu in the ERPLAB menu ('Data Quality options') allows access from the EEGLAB-ERPLAB GUI.
- A new table interface to show all the data quality information from an ERP set with `DQ_Table_GUI(ERP)` or through the above GUI menu option.
- These data quality metrics can be summarized on the Command Window, saved to Mat structure or exported to Excel, or plotted in the above interactive table.
- The data quality information and metadata is stored in a new structure, ERP.dataquality

<br/>
<br/>

- New options for calculating, viewing, and saving, frequency spectra, in the `compute_fourier(EEG)` [function](https://github.com/lucklab/erplab/wiki/Generate-Frequency-Spectra)

<br/>
<br/>

- Various [bugfixes](https://github.com/lucklab/erplab/commits/master)

- Older [release Notes can be found here](https://github.com/lucklab/erplab/wiki/Release-Notes)




## ERPLAB v7.0.0 Release Notes

- Updated tools for [pre-processing continuous EEG](https://github.com/lucklab/erplab/wiki/Continuous-EEG-Preprocessing), including functions for
   - deleting time segments
   - shifting event codes
   - selective electrode interpolation

- Crucial [compatibility fixes](https://github.com/lucklab/erplab/issues/56) to allow running in R2017b and later, while still being backwards-compatible with older versions of Matlab. No more yellow warnings about NARGCHK in R2016a or later.




### ERPLAB v6.1.4
Some additions and minor bugfixes, including:
- Removing channels can now avoid deleting all channel location information
- More channel location tools
- Measurement Window GUI now fits on a smaller screen
- Improvements in 'Preprocess Continuous EEG' options
- Fixed a bug where the number of loaded erpsets would be mistakenly taken to be zero
- Improved Current-Source-Density compatibility
- Replaced the error 'Quack' noise with a beep, and replaced some error pictures.

### ERPLAB v6.1.3
Minor bugfixes, including:
- Cleaned up the Measurement Viewer text and options
- Measurement Viewer helper text now only shown when relevant

### ERPLAB v6.1.2
Minor bugfixes, including:
- Fixed BDF Library url-link in BDF-Visualizer
- Swapped artifact and user-flag display in BDF-Visualizer

### ERPLAB v6.1.1
Minor bugfixes, including:
- Shift Event Codes GUI fix - now doesn't crash on launch.
- Adopted [Major].[Minor].[Patch] version numbers, this being v6.1.1, with backward-compatible file loading. Note - from v6.0, we no longer indicate the file type usage in the version number, and this is now always taken to be 1.

### ERPLAB v6.0 Release Notes

With ERPLAB v6.0, we include a variety of new features, user-interface improvements, bug-fixes, and improvements to existing functions. Among these, we have:


### - Current Source Density Tool

EEG or ERP data can be used to compute an estimate of the Current Source Density (CSD). We include new functions to take data loaded in ERPLAB (either EEG or ERP) and compute the CSD data. We use CSD methods from Jürgen Kayser (from the [CSD Toolbox](http://psychophysiology.cpmc.columbia.edu/Software/CSDtoolbox/)).

These tools can be found in the new 'ERPLAB -> Data Transformations' menu. A new ERPLAB dataset is generated, with CSD data in the place of EEG/ERP data.

Find [CSD documentation here](https://github.com/lucklab/erplab/wiki/Current-Source-Density-(CSD)-tool)


### - Fractional peak measurement can now be offset (post-peak) as well as onset (pre-peak)

In the ERP Measurement tool, ERPLAB can record measurements of local peaks and the time of a fractional peak, like 50% peak. Previously, this fractional peak measurement was taken from the 'onset' of the peak, before the peak. In v6.0, ERPLAB also has an option to measure the fractional peak 'offset', the 50% peak value after the peak.



### - ERPLAB documentation on GitHub

For more easy editing, ERPLAB documentation has been moved to a [wiki here](https://github.com/lucklab/erplab/wiki).



----
### Bug Fixes

[Bug fixes as detailed here](https://github.com/lucklab/erplab/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aclosed)
