However, it is sometimes useful to delete "crazy" sections of the continuous EEG (e.g., prior to performing ICA). Procedures for this are described on this page. Note that these procedures actually delete sections of data (as opposed to simply marking them for rejection). Note that you should not use these procedures for "ordinary" artifacts (eye blinks, etc.); you should ordinarily detect these artifacts in the epoched data (see previous section).

Note that the deletion of sections of the EEG also leads to deletion of the event codes within those sections. Consequently, if you are going to delete sections of EEG (with any method), you must do so before the EVENTLIST has been created.


### Delete Time Segments 

The function `Delete Time Segments` deletes segments of continuous EEG data between event codes if the length of the segment is greater than a user-specified length of time

- Located in `ERPLAB > Preprocess Continuous EEG Data > Delete Time Segments`
- Input
  - **Min Time Threshold**: Minimum length of time between consecutive event codes to delete data
  - **Start Event Code Buffer**: Length of time around the first event code to save
  - **End Event Code Buffer**: Length of time around the end event code to save
- Optional Input
  - **Ignore event codes**: Numeric event code numbers to ignore
  - **Display EEG**: Plot the EEG data with the to-be deleted data marked 
- Related Pop Function: `pop_erplabDeleteTimeSegments`
  - `EEG = erplab_deleteTimeSegments(EEG, inputMaxDistanceMS, inputStartPeriodBufferMS, inputEndPeriodBufferMS, ignoreEventCodes);`
  - Example: Delete data segments between any two event codes when it is longer than 3000 ms (3 secs).
    - ```EEG = erplab_deleteTimeSegments(EEG, 3000, 100, 200, []);```

----
### Shift Event Codes 

The `Shift Event Codes` function moves the timing of user-specified event codes either forward or backwards in time. This is mainly used to counter the delay between stimulus presentation on a monitor and the onset of the subsequent stimulus event code. 
 
- Location: `ERPLAB > Preprocess Continuous EEG Data > Shift Event Codes`
- Input:
  - **Event codes**: list of event codes to shift
  - **Timeshift**: Amount of time to move the event code either forwards/backwards in time
    - If timeshift is positive, the EEG event code time-values are shifted to the right (e.g. increasing delay).   
    - If timeshift is negative, the event code time-values are shifted to the left (e.g decreasing delay).
    - If timeshift is 0, the EEG's time values are not shifted.
  - **Rounding**: Type of rounding to use
    - 'earlier'    (default) Round to the earlier timestamp          
    - 'later'      Round to later timestamp
    - 'later'      Round to nearest nearest
  - **Display EEG**        - true/false  - Display a plot of the EEG when finished

- Related POP-function: `pop_erplabShiftEventCodes`
  - `EEG = pop_erplabShiftEventCodes(inEEG, eventcodes, timeshift)` 
  - Example:
    ```Matlab
    eventcodes = {'22', '19'};
    timeshift  = 0.015;
    rounding   = 'floor';
    outputEEG  = erplab_shiftEventCodes(inputEEG, eventcodes, timeshift, rounding);
    ```     

-----
### Interpolate Electrodes

pop_erplabInterpolateElectrodes Replace specific electrodes in continuous EEG data through interpolation with the option to ignore specific channels
Format
   EEG = pop_erplabInterpolateElectrodes(inEEG, replaceChannels, ignoreChannels)
* Input
  * EEG: EEG dataset
  * replaceChannels: list of event codes to shift
  * ignoreChannels:  time in sec. 
    * If ignoreChannels is positive, the EEG event code time-values are shifted LATER (e.g. increasing delay).
    *  If ignoreChannels is negative, the event code time-values are shifted EARLIER to the left (e.g decreasing delay).
    * If ignoreChannels is 0, the EEG's time values are not shifted.
  * interpolationMethod: Type of interpolation method to use
    * 'nearest'    (default) Round to the nearest integer          
    * 'floor'      Round to nearest ingtowards positive infinity
    * 'ceiling'    Round to nearest integer towards negative infinity
* Optional Input
  * displayFeedback: Type of feedback to display at Command window
    * 'summary'   (default) Print summarized info to Command Window
    * 'detailed'  Print event table with latency differences
    * 'both'      Print both summarized & detailed info
* Output
  * EEG               EEGLAB EEG dataset with the specified channels replaced through interpolation
* Example
```Matlab 
replaceChannels       = {'22', '19'};
ignoreChannels        = 0.015;
interpolationMethod   = 'floor';
outputEEG             = pop_erplabInterpolateElectrodes(EEG, replaceChannels, ignoreChannels, interpolationMethod);
```     

