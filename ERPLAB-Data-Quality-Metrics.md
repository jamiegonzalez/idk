## Overview
As of ERPLAB v8.0, ERPLAB contains multiple routines designed to allow users to quantify the quality of their data. This page provides a general overview of how these routines work together. Details of implementation are provided in the manual pages for the [Averaging routine](https://github.com/lucklab/erplab/wiki/Computing-Averaged-ERPs) and the [Grand Averaging routine](https://github.com/lucklab/erplab/wiki/Averaging-Across-ERPSETS-(Creating-Grand-Averages)). Here, we provide the big picture.

### Data Quality Metrics
At present, we directly support three classes of metrics of data quality:
1. **Baseline noise** - the noise level during the baseline period for each waveform in an ERPset. This is typically quantified as the standard deviation of the voltage values during the baseline period. It provides a generic measure of the amount of noise that remains in the data after averaging.
2. **Pointwise SEM** - The standard error of the mean at each time point for each waveform in an ERPset (i.e., each combination of bin and channel). This can be either the standard error across trials for a single-participant averaged ERP waveform or the standard error across participants for a grand average. This is a common way of visualizing the noise (using ERPLAB > Plot ERPs > Plot ERP Waveforms), but it is less useful as a quantitative metric.
3. **SME** - The standardized measurement error (SME) for one or more amplitude or latency “scores”. A score would be something like “mean amplitude from 300-500 ms,” “peak latency from 200-800 ms,” or even “50% area latency from a difference wave.” The SME quantifies the standard error of measurement for that specific score. A given type of noise will impact some types of scores more than others. For example, high-frequency noise has much more impact on a peak amplitude score than on a mean amplitude score. The SME quantifies the noise that directly impacts whatever score you are actually using as the dependent variable in your final analyses.

### Standardized Measurement Error - Analytic SME (aSME) and Bootstrapped SME (bSME)
If you are scoring the amplitude of an ERP component as the mean voltage during some time window (e.g., quantifying P3 amplitude as the mean voltage between 300 and 500 ms), the SME can be automatically calculated using a simple equation during averaging. We call this the analytic SME or aSME. By default, ERPLAB computes aSME at the point of ERP averaging, in. The time windows in which it is computed can be customized, and are 100 ms windows, centered around 0 ms, by default.

For types of scores where analytic SME does not easily apply (like peak amplitude scores, or any score using latency measures), the process of bootstrapping can be used to compute the SME. In this case, we specify this as bootstrapped SME (bSME). This is not computed by default, but can be added via simple Matlab scripts.


## What is the purpose of the data quality metrics?
Data quality metrics are initially computed for each participant at the time of averaging, but you can obtain aggregate values for a group of participants when you make a grand average. 

The single-participant data quality metrics can be used to determine whether the data from a specific participant, channel, or bin are especially noisy. For example, you might use the SME value from a given channel to determine if any channels are “bad” and should be interpolated for a given participant. You might also use this value to determine whether a given participant’s data are so noisy that the participant should be excluded from the final analyses of a study (although this should be done only when you have an a priori criterion for deciding how bad the noise must be for a participant to be excluded).

When aggregated across a group, the SME can tell you how much of the overall variance in your amplitude or latency score is a result of measurement error. The aggregated SME also allows you to compare data quality across experimental paradigms, across laboratories, across recording systems, across research assistants, and across signal processing methods.

For more information about what the SME value means and how you can use it, see  this paper:

Luck, S. J., Stewart, A. X., Simmons, A. M., & Rhemtulla, M. (2019). _Standardized Measurement Error as a Universal Measure of Data Quality for Event-Related Potentials: An Overview._ BioRxiv. https://doi.org/10.31234/osf.io/jc3sd

We encourage you to report the aggregated SME values in your publications (and please cite our paper when you do so!). If SME values become common in publications, this will make it possible for the field to determine what recording and analysis procedures lead to the highest data quality, which will allow everyone to improve the quality and reproducibility of their research.

