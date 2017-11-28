
# Make Standard Error of the Mean (SEM) set

**ERPLAB -> Datatype Transformations -> Move Standard Error of the Mean (SEM) to be primary data**

When running the ERP Averager on bin-epoched EEG data, there is an option to calculate the Standard Error of the Mean SEM across these trials, at each electrode and timepoint. This option is on by default, and saves SEM to the ERP.binerror field. This can be used for plots like these, showing the SEM around an ERP plot.


Additionally, you might wish to examine this SEM data in detail. Choosing this option moves the ERP.binerror data to ERP.bindata, and so the SEM data can be plotted in ERPLAB and measured in the ERPLAB Measurement Window as if this were ERP data.
