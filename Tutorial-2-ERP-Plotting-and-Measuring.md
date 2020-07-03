In the first section of the ERPLAB tutorial, we demonstrated [loading EEG data, assigning data to bins, and making a new ERP dataset with these bins.](https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset). Here, we look at ERPLAB functions for plotting and measuring this ERP dataset.

With an ERP set loaded, the EEGLAB window will show entries in **ERPsets** menu. Functions will primarily apply to the selected ERP set, which is S1_ERP.erp below. If you don't have an ERPset loaded already, hit `ERPLAB menu > load existing ERPset`.

![ERPsets_menu](https://user-images.githubusercontent.com/5137405/86484381-f40c7080-bd0a-11ea-9a39-688525a4abaf.png)

_ERPsets menu showing that S1_ERP is loaded and active._

# Viewing vs Plotting vs Measuring

ERPLAB has many options for plotting ERP data. In order to explore your ERP dataset, showing different channels and bins, and scrolling through them quickly, we have the `ERP Viewer`. To produce ERP plots at figures, which can be tailored in appearance and exported as PDFs, we have the `ERP Plot Waveform` tool. For recording specific values from the ERP, such as mean within a time range, we have the `ERP Measurement Tool`. Let's examine each of these in turn.

# ERP Viewer

To run, hit `ERPLAB menu > ERP Viewer`.

![ERP_Viewer1](https://user-images.githubusercontent.com/5137405/86485942-e3f69000-bd0e-11ea-8ddb-81805913d3ba.png)

The ERP Viewer is useful for quickly exploring you ERP data. Note that, using the button selectors on the right (`<`,`>`), you can choose which of your ERP bins to plot, or tick the corresponding box to plot `all` Bins. Likewise, for those selected Bins, you can plot data from any single EEG channel, or all EEG channels (Channel 1, F3, is plotted first in the above example).

The time range can be customized in the top right. By default, this will first select the entire epoch. With the `S1_ERP` from the [example datasets](https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset#download-example-eeg-data-set), an epoch length of `-200` ms to `+800 ms` was chosen, which rounds down the 798 ms shown above.

The Y range can also be changed in the top right. Typically, this is µV. Enter two numbers here to change the Y range, in the format `min max`, so `-20 20` to show from -20 µV to +20 µV.

Note that the panel on the on the lower left shows information about the current plot. Additionally, you can click the tickbox to enable 'Adjust measurement time`, click on a new time point, and information will be updated to show the time and value there.

Here, we select all Bins, Channel 6 (P4), and click on 442 ms:
![ERP_Viewer_click](https://user-images.githubusercontent.com/5137405/86488208-15725a00-bd15-11ea-8244-1ab9d3f32ddb.png)

<br><br>

# Plot ERP Waveforms







