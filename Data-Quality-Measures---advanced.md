Here we show more information about the Data Quality measures in ERPLAB.

## The ERP.dataquality structure
By default, the ERP Averager produced an ERP dataset with 3 dataquality measures. They are saved in the Matlab structure *ERP.dataquality* - ERP.dataquality(1), ERP.dataquality(2), and ERP.dataquality(3).

![ERPdq_struct](https://user-images.githubusercontent.com/5137405/77694613-8d3b2680-6f67-11ea-97e6-be2128aefa1e.png)

They have the fields of __type (string), times (tw x 2 array, start times, end times, where tw is the number of time windows), data (electrodes x tw x bin), time_window_labels (optional cell array of strings, length of tw), and comments (optional string).

