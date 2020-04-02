As [ERPLAB v8](https://github.com/lucklab/erplab/releases), ERPLAB includes new features to assess data quality. For an [overview of data quality, see here.](https://github.com/lucklab/erplab/wiki/ERPLAB-Data-Quality-Metrics)

By default, several measures are included -- baseline variability, pointwise SEM, and Analytic Standardized Measurement Error (aSME). These are calculated at the point of running the ERP Averager on a bin-epoched EEG dataset, when an ERP dataset is first created.

![ERPLAB_v8_AVG](https://user-images.githubusercontent.com/5137405/77691462-2f581000-6f62-11ea-9a33-2c702bf606c8.png)

These measures, their parameters, and time-windows can be customized by setting '**On - custom parameters**' at the ERP Averager, and selecting '**Set DQ options**'.

## Seeing the DQ Measure information

There are multiple options for seeing this data quality information. This can be shown in an interactive table, where measures and bin can be selected, or in summary statistics to the Matlab Command Window, or saved to a separate file (Excel spreadsheet, or Matlab file).

![ERPLAB_DQ_menu2](https://user-images.githubusercontent.com/5137405/77691887-e8b6e580-6f62-11ea-9eb7-1ee73effe764.png)

![DQ_Table_GUI](https://user-images.githubusercontent.com/5137405/77692310-a17d2480-6f63-11ea-9279-60ade4bf42c8.png)

In the active ERP dataset, the data quality information is saved in the ERP.dataquality Matlab structure. For more information, see the [description here.](https://github.com/lucklab/erplab/wiki/Data-Quality-Measures---advanced) 