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
For more involved plots, we have the Plot ERP Waveforms tool.

Hit `ERPLAB menu > Plot ERP > Plot ERP Waveforms`.

![ERP_plot](https://user-images.githubusercontent.com/5137405/86488424-c7118b00-bd15-11ea-8b7e-67e1053654b0.png)

Here, a new Matlab figure will be produced, plotting your ERP data, with options set as needed.

![ERP_plot_se](https://user-images.githubusercontent.com/5137405/86490236-8b79bf80-bd1b-11ea-855d-7089efe4c931.png)


By default, all Bins will be plotted, as shown in the top left. You can change this, entering the index number of desired bins or bin ranges (as `1:4` for all bins 1 thru 4) in the text entry field on the top left.

The channels to plot can be customized on the panel on the top right. Here, we have all channels, 1:16 for S1_ERP.

The time range, amplitude Y range, and plot ticks for each can be tailored on the panel on the left. We also see an option for plotting `show standard error` on the lower left. For standard error, we suggest plotting at size x1 and transparency of 0.6.

Plotting S1_ERP with these parameters gives:

<br>

<a href="https://user-images.githubusercontent.com/5137405/86490039-ed85f500-bd1a-11ea-9542-f46b4daf521c.png">
 <img src="https://user-images.githubusercontent.com/5137405/86490039-ed85f500-bd1a-11ea-9542-f46b4daf521c.png" alt="ERP plots - click for bigger image";
style="cursor:pointer;"
     title="ERP plots - click for bigger image">
</a>

_ERP Plots - click for bigger image_

Note that all 16 channels are shown in different subplot, labelled with channel name. Below, there is a legend showing the color of each ERP bin, with it's name, and label.

Clicking (or double-clicking, depending on OS/Matlab) on a subplot of a single channel in the above plot will show the ERP for that channel in more detail:

<a href="https://user-images.githubusercontent.com/5137405/86490548-984ae300-bd1c-11ea-862d-722342b0589e.png">
 <img src="https://user-images.githubusercontent.com/5137405/86490548-984ae300-bd1c-11ea-862d-722342b0589e.png" alt="ERP plot P4 - click for bigger image";
style="cursor:pointer;"
     title="ERP plot P4 - click for bigger image">
</a>

_ERP Plot P4 only - click for bigger image_

### Export to graphics program
While there are many options for showing your ERP data and customizing plots, we recommend exporting these figures as PDFs and tailoring the presentation of your plots before including them in a publication. For that purpose, note the PDF icon in the top right . With the PDF or .eps file written, you can edit this in the graphics program of your choice (like Photoshop, Inkscape, [Affinity Designer](https://affinity.serif.com/en-us/designer/), or LibreOffice Draw). Text style and figure structure can then be tweaked in the graphics program to create publication-ready figures (as [detailed in the Intro to ERP book](https://mitpress.mit.edu/books/introduction-event-related-potential-technique-second-edition)).

![Affinity_gfx](https://user-images.githubusercontent.com/5137405/86491343-6dae5980-bd1f-11ea-945c-449f2669d3ff.png)



<br><br>


# ERP Measurement Tool

Another important aspect of ERPLAB is to obtain specific measurements from ERP datasets. 

Hit `ERPLAB menu > ERP Measurement Tool`.

![Measurement_tool_GUI](https://user-images.githubusercontent.com/5137405/86493440-722a4080-bd26-11ea-81bc-8f9b733db22d.png)

On the panel on the left, we see options for which ERPset it is that will be measured. While this could be a list of several ERPsets, let's examine the single ERPset of S1_ERP now, through selecting `Current ERPset` or `From ERPset menu: 1`.

On the right, we first select the type of measurement desired. Let's select `Mean amplitude between two fixed latencies`. For this measure, we will provide two times (in ms), and the mean value (amplitude, in µV) will be recorded for all selected Bins and Channels. These Bins and Channels of interest are specified in the mid-right.

It is essential to enter two times for this measure - the start and the end time of the measurement window in milliseconds. For other types of measure (like from a single time), then only one number is need for the measurement window.

On hitting `RUN`, measurements will be taken from the selected ERPsets. Those values can be written to a text file (provide a file name, like `measurements_written.txt`, or a full path, in the output file box), or alternatively, written to a ERP_Measures variable in the Matlab workspace.

## ERP Viewer for Measurements

Additionally, the ERP Viewer tool can also be used with the Measurement Tool.

If the values above are entered, and the `Viewer` is selected in the ERP Measurement Tool, then those values can be previewed and instantantly viewed in ERP Viewer. Notice that the info panel in the lower left now shows the corresponding window of interest, and the value of the measurement.

![Measurement_Viewer](https://user-images.githubusercontent.com/5137405/86493884-13fe5d00-bd28-11ea-858d-3b1fb479258b.png)


