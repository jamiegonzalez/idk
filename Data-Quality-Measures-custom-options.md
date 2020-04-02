For an [overview of data quality, see here.](https://github.com/lucklab/erplab/wiki/ERPLAB-Data-Quality-Metrics)

The ERP Averager can compute some data quality measures.

## Setting custom DQ parameters
The parameters, including time window length and range, can be customized through selecting **On - custom** at the ERP Averager:

![E8_avg_dq_custom_on](https://user-images.githubusercontent.com/5137405/78295457-0515cd80-74e1-11ea-99e9-27cf12592033.png)


This will make the **Set DQ options** button available. Hit this to bring up the following window:

![E8_set_custom_dq_options](https://user-images.githubusercontent.com/5137405/78295614-44441e80-74e1-11ea-927c-7e1bb8ac7e8f.png)

This shows 3 sections, corresponding to the 3 measures of:

1. **Baseline noise** 

2. **Pointwise SEM** 

3. **SME**

The tick-boxes on the left indicate the whether each measure should be included -- all on by default.

### **Baseline noise** customization
The default time range for baseline variability is from the start of the ERP epoch up to 0 ms. For example, if the ERP epoch ran from 250 ms before the epoch anchor event until 1000 ms after, then the default baseline variability time period for measuring here would be `-250:0`. If you wish to set a custom time period, set the custom time period radio button, then the time (in ms) of the start of the window, and then the time of the end of the window.

Baseline variability can be set in either standard deviation (default) or [root-mean square combination](https://www.mathworks.com/help/signal/ref/rms.html).

### **aSME** customization
SME is computed on a 'score' -- a defined measure, rather than on each datapoint. By default, we take aSME of mean amplitude on non-overlapping 100 ms windows. This is calculated for each electrode, and each bin, in each ERP dataset.

In this table, you can choose to customize the number of aSME submeasures. The first editable column specifies a custom text label for the aSME submeasure. The second and third editable columns gives the start and end of each time window.

The buttons at the bottom of the table allow adding a line, or removing the selected line.

### Accessing custom DQ
With these options set, complete running the ERP Averager.

With the new ERP structure generated, you can see the DQ information. See [here for DQ viewing and saving info](https://github.com/lucklab/erplab/wiki/ERPLAB-Data-Quality-Metrics#viewing-and-saving-the-data-quality-measures).

The custom specification is also reflected in the DQ metadata shown in the ERP structure, [as shown here](https://github.com/lucklab/erplab/wiki/Data-Quality-Measures---advanced).


 