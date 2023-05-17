# Selecting Optimal Filters with ERPLAB Toolbox
Using an appropriate filter can dramatically increase your effect sizes and your
statistical power. However, an inappropriate filter can dramatically distort your ERP waveforms,
leading to bogus effects and completely false conclusions. The optimal filter settings will depend
on the nature of your research participants, the kinds of experiments you run, the quality of your
recording setup, and the specific amplitude or latency scores that you will be analyzing. How can
you determine the optimal filter settings for your data?<br><br>
We have developed an approach for selecting optimal filter settings, <REF> along with
ERPLAB tools that make it relatively simple for you to apply this approach to your own data.
We have also applied this approach to the [ERP CORE](https://osf.io/thsqg/), which includes data from 40 healthy
young adults who performed six standardized paradigms that yielded seven commonly-studied
ERP components. If you are analyzing reasonably similar data, you can simply use the settings
we developed using the ERP CORE data. The table below shows these recommended settings
<see REF for a detailed description>. Note that different filter settings are optimal for different
components and different scoring methods.<br>

If your study is a bit different from the ERP CORE, these settings should still be
reasonably close to optimal for your data. However, if you are using a very different participant
population (e.g., young infants), a very different recording setup (e.g., dry electrodes), or very
different ERP components (e.g., auditory brainstem responses), you may need very different
settings. The purpose of this document is to explain exactly how to use ERPLAB to determine
the optimal settings for your data. This will take a fair amount of time, but once you have done it,
you can use the same filter settings for any reasonably similar dataset.<br>

### Brief Overview of the Approach
We define the optimal filter as the one that maximizes data quality while minimizing
waveform distortions. Our approach begins by applying a large number of filters with different
low-pass and high-pass cutoff frequencies to a given dataset to quantify the data quality yielded
by each filter. We then assess the amount of waveform distortion produced by each filter. We
then select the filter that produces the best data quality without exceeding a threshold for
waveform distortion.<br>

Our approach to quantifying data quality uses the _standardized measurement error_ (SME), which assesses the noise level of a given participant’s data with respect to a specific
amplitude or latency score. A smaller SME means lower noise, and filters generally decrease the
SME. You can read more about the SME at:<br>
* Blog post: [A New Metric for Quantifying ERP Data Quality](https://erpinfo.org/blog/2020/4/28/data-quality)
* Published paper: [Standardized measurement error: A universal metric of data quality for averaged event-related potentials
](https://onlinelibrary.wiley.com/doi/10.1111/psyp.13793)<br>

For latency scores (e.g., peak latency, 50% area latency), we simply use the SME to
quantify the data quality resulting from a given filter. For amplitude scores (e.g., peak amplitude,
mean amplitude, area amplitude), a filter may reduce the score (the _signal_) in addition to
reducing the noise, and it is important to assess the reduction in noise relative to the reduction in
signal. Thus, our approach uses the _signal-to-noise ratio_ (SNR) to evaluate the effects of filters
on amplitude scores. The signal is defined as the score itself, and the noise is defined as the SME
for that score. When the SNR is quantified in this manner, we refer to it as the SNR<sub>SME</sub>.<br>

Whenever possible, we recommend using difference waveforms (e.g., rare-minus-
frequent for the P3 wave, faces-minus-cars for the N170, contralateral-minus-ipsilateral for N2pc
and LRP) to assess waveform distortion and quantify the signal and the noise. This will allow you to assess how the filter impacts your experimental effect and decide on a single filter for all
experimental conditions. If you are studying multiple groups, you should collapse across groups
as well so that you can decide on a single filter for all groups.<br><br>
Filters inevitably distort ERP waveforms, and our approach involves quantifying the
amount of waveform distortion. We do this by creating a simulated waveform that resembles the
effect of interest and examining the distortion produced when this waveform is filtered. It is
necessary to use simulated waveforms rather than real data to assess waveform distortion
because the true waveform is not known for real data. The most problematic type of waveform
distortion produced by typical ERP filters is the introduction of artifactual peaks before or after
the true peaks. We quantify this by computing the artifactual peak percentage, which is the
amplitude of the artifactual peak as a percentage of the amplitude of the true peak (after
filtering).<br>

### Quantifying waveform distortion
We recommend quantifying waveform distortion first. This step is relatively simple and
fast, and it will allow you to focus the more time-consuming steps on filters that create
acceptable levels of distortion. To assess waveform distortion, you must create an artificial ERP
waveform that approximates the true waveform. Of course, you don’t know the true waveform,
but the simulated waveform does not need to be an exact match.<br>

You can create a simulated waveform using ERPLAB > Create Artificial ERP
Waveform. It allows you to create a Gaussian waveform (which is good for most perception-
related components) or ex-Gaussian waveform (a skewed version of a Gaussian, which is good
for most cognitive components). The function allows you to overlay the artificial data with a real
ERPset (usually a grand average difference wave) so that you can visually adjust the parameters
of the simulated waveform until it matches the real data. If the real waveform is complex (e.g., a
negative-going ERN followed by a positive-going Pe), you can either try to simulate one portion
of if (e.g., just the ERN), or you can simulate multiple components individually and then sum
them together (by saving each waveform in a separate file, appending them into a single ERPset
using ERPLAB > ERP Operations > [Append ERPsets](https://github.com/lucklab/erplab/wiki/Appending-ERPSETS), and then summing them using ERPLAB > ERP Operations > [ERP Bin Operations](https://github.com/lucklab/erplab/wiki/ERP-Bin-Operations)).<br>

Once you have created the simulated waveform, you can apply each filter you would like
to test using ERPLAB > Filter & Frequency Tools > [Filters for ERP Data](https://github.com/lucklab/erplab/wiki/Filtering-EEG-and-ERPs:-Tutorial). You can apply a given
combination of low-pass and high-pass filters simultaneously. Ordinarily, it’s not a good idea to
apply high-pass filters to averaged ERP waveforms because of the potential for edge artifacts.
However, this will not be a problem with artificial data as long as you simulate a sufficiently
long epoch (e.g., -2000 to +2000 ms) and make sure that the simulated component reaches zero
well before the beginning and end of the epoch.<br>

If you plot the filtered waveforms, you should be able to see the distortion produced by
the filter (hint: if you want to overlay the filtered and unfiltered waveforms, you must first
append them into the same ERPset using ERPLAB > ERP Operations > [Append ERPsets](https://github.com/lucklab/erplab/wiki/Appending-ERPSETS)). You
can then quantify the amplitude distortion using ERPLAB > [ERP Measurement Tool](https://github.com/lucklab/erplab/wiki/ERP-Measurement-Tool). You will
want to find the positive peak amplitude over the entire epoch and find the negative peak
amplitude over the entire epoch (for the filtered waveform). These numbers can then be
converted into the _artificial peak percentage_, which is 100 times the absolute value of the peak
voltage of the artifactual peak divided by the absolute value of the peak voltage of the true peak.
For datasets recorded from highly cooperative subjects (e.g., college students) using a high-quality recording system in most standard paradigms, we recommend using filters that produce less than 5% distortion. For much noisier datasets, a higher threshold would be reasonable.<br>

### Quantifying the noise with the standardized measurement error (SME)
The next step is to quantify the noise using the SME for each filter you wish to consider.
You will obtain an SME value from each individual participant, and then you will aggregate
across individuals using the root mean square (RMS) of the single-participant values. See Manual > [Data Quality Metrics](https://github.com/lucklab/erplab/wiki/ERPLAB-Data-Quality-Metrics)
for detailed information about how to compute the SME in ERPLAB. You should apply all of
your usual preprocessing steps (e.g., re-referencing, filtering, artifact correction/rejection) prior
to computing the SME. You will therefore need to preprocess your data separately for each filter
you wish to test. If you are using ICA-based artifact correction, we recommend computing the
ICA coefficients once and then transferring them to each filtered dataset before removing the
artifactual components ([see Chapter 9 in Luck, 2022](https://socialsci.libretexts.org/Bookshelves/Psychology/Book:_Applied_Event-Related_Potential_Data_Analysis_(Luck))).<br>

**SME for mean amplitude scores**<br>
ERPLAB makes it easy to compute the SME values for
mean amplitude scores. When you average the data using ERPLAB > Compute averaged ERPs,
you simply select “On – custom parameters” in the Data Quality Quantification section of the
averaging GUI, and customize the aSME data quality measures to include the time window that
you are using to compute your mean amplitude scores (e.g., 300-600 ms for the P3 wave). The
ERPset created by averaging will then contain the SME values for this time window. To get the
SME value for a difference between two conditions, you can use this equation: SME<sub>A-B</sub> =
sqrt(SME<sub>A2</sub> + SME<sub>B2</sub>). SME<sub>A-B</sub> is the SME of the difference between conditions A and B, and
SME<sub>A</sub> and SME<sub>B</sub> are the SME values from the two individual conditions. Note that this equation
applies only when the score is the mean voltage across a time window and when the difference
wave is between waveforms from separate trials (e.g., rare minus frequent for P3, unrelated
minus related for N400). You must instead use bootstrapping if you are scoring a difference
between two electrode sites (e.g., contralateral minus ipsilateral for N2pc) or looking at some
other score (e.g., peak amplitude, 50% area latency).<br>

**Bootstrapped SME values**<br>
If you are unable to use the simple approach described in the
previous paragraph, you can instead using bootstrapping to obtain the single-participant SME
values. At present, this requires scripting. You can find an overview of how to compute
bootstrapped SME values in Luck et al. (2021), and you can see example scripts at
https://osf.io/a4huc/. You can learn how to write EEGLAB/ERPLAB scripts by reading [Chapter 11 of Luck (2022)](https://socialsci.libretexts.org/Bookshelves/Psychology/Book:_Applied_Event-Related_Potential_Data_Analysis_(Luck)).<br>

**Choosing electrode sites**<br>
You will get separate SME scores for different electrode sites.
In terms of selecting an optimal filter, the exact electrode site shouldn’t matter much, and the
simplest thing to do is to use the channel in which the effect is largest. You could also collapse
across a set of channels prior to averaging (using EEG Channel Operations) to create a clustered
channel, and then you could obtain the SME value from this clustered channel.<br>

**Aggregating across participants**<br>
Once you have the single-participant SME scores, you
can combine them into a single RMS(SME) value by squaring the SME values, summing the
squared values together, and then taking the square root of this sum.<br>

### Quantifying the SNR<sub>SME</sub> for amplitude scores
For amplitude scores, you will need to take the RMS(SME) value from the previous step
and use it to compute the SNR<sub>SME</sub>. This is quite simple. Using ERPLAB’s [Measurement Tool](https://github.com/lucklab/erplab/wiki/ERP-Measurement-Tool),
you simply measure the score of interest from the grand average waveform (preferably a
difference waveform). This is done separately for each filter you are evaluating. The SNR<sub>SME</sub> for
a given filter is then computed by dividing this score by the RMS(SME) value for that filter. You do not need the SNR<sub>SME</sub> value when dealing with latency scores. You will simply use the RMS(SME) value.<br>

### Final filter selection
For amplitude scores, you will select whatever filter produced the largest SNR<sub>SME</sub> value
while not exceeding the maximal acceptable artificial peak percentage (e.g., 5%). For latency
scores, you will select whatever filter produced the smallest RMS(SME) value while not
exceeding the maximal acceptable artificial peak percentage (e.g., 5%).
