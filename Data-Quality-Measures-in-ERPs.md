As [ERPLAB v8](https://github.com/lucklab/erplab/releases), ERPLAB includes new features to assess data quality.

By default, several measures are included -- baseline variability, pointwise SEM, and Analytic Standardized Measurement Error (aSME). These are calculated at the point of running the ERP Averager on a bin-epoched EEG dataset, when an ERP dataset is first created.

![ERPLAB_v8_AVG](https://user-images.githubusercontent.com/5137405/77691462-2f581000-6f62-11ea-9a33-2c702bf606c8.png)

These measures, their parameters, and time-windows can be customized by setting '**On - custom parameters**' at the ERP Averager, and selecting '**Set DQ options**'.