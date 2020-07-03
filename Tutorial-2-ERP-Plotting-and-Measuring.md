In the first section of the ERPLAB tutorial, we demonstrated [loading EEG data, assigning data to bins, and making a new ERP dataset with these bins.](https://github.com/lucklab/erplab/wiki/Tutorial-1-EEG-to-ERPset). Here, we look at ERPLAB functions for plotting and measuring this ERP dataset.

With an ERP set loaded, the EEGLAB window will show entries in **ERPsets** menu. Functions will primarily apply to the selected ERP set, which is S1_ERP.erp below. If you don't have an ERPset loaded already, hit `ERPLAB menu > load existing ERPset`.

![ERPsets_menu](https://user-images.githubusercontent.com/5137405/86484381-f40c7080-bd0a-11ea-9a39-688525a4abaf.png)

_ERPsets menu showing that S1_ERP is loaded and active._

# Viewing vs Plotting vs Measuring

ERPLAB has many options for plotting ERP data. In order to explore your ERP dataset, showing different channels and bins, and scrolling through them quickly, we have the `ERP Viewer`. To produce ERP plots at figures, which can be tailored in appearance and exported as PDFs, we have the `ERP Plot Waveform` tool. For recording specific values from the ERP, such as mean within a time range, we have the `ERP Measurement Tool`. Let's examine each of these in turn.

# ERP Viewer

To run, hit `ERPLAB menu > ERP Viewer`.

![ERP_Viewer1](https://user-images.githubusercontent.com/5137405/86485942-e3f69000-bd0e-11ea-8ddb-81805913d3ba.png)


