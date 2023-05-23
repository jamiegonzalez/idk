ERPLAB -> Create Artificial ERP Waveform is used to simulate the waveform for a given ERP component, which can then be saved as an ERPset. 

The basic idea behind this tool is to allow users to define a set of parameters to generate an artificial ERP waveform that either mimics real data or has other useful properties. Users can also  add various types of random noise to this artificial waveform, such as sinusoidal noise, white noise, and pink noise. 

To facilitate the comparison between the artificial waveform and real ERPs, the tool provides an option to load a pre-existing ERP. The GUI is shown in the screenshot below: 

![Screen Shot 2023-05-22 at 1 06 15 PM](https://github.com/lucklab/erplab/assets/97117923/6cfd6032-e521-44e6-afab-28ed976e419d)

This tool allows you to generate artificial waveforms using three functions, the options for which can be found at the bottom of the GUI. You can only use one function at a time, so the parameters for the other two functions will be grayed out once you have selected which function you want to use. 

## Function types

Here are the different types of functions that can be generated:

**Ex-Gaussian (and Gaussian)**
- An ex-Gaussian function is a Gaussian function convolved with an exponential function, which skews the waveform rightward or leftward.
- The SD parameter controls the width of the Gaussian, and the Gaussian mean parameter controls the horizontal shift of the Gaussian. The tau parameter is the time constant of the exponential function (in milliseconds), which controls the decay rate. A negative tau creates a leftward shift and a positive tau creates a rightward shift.
- To create a standard Gaussian function, simply set the exponential tau value to zero.
- A pure Gaussian is good for most perception-related components, in which the waveform is symmetrical.
- An ex-Gaussian function with a rightward skew is good for most cognitive components. A leftward skew is typically used for response-locked averages in which the onset of the component of interest precedes the response (e.g., the P3b wave in a response-locked average).

**Impulse**
- An impulse has a value of the desired peak amplitude at the desired latency and a value of zero at all other time points. This can be used to assess the impulse response function of a filter.

**Boxcar**
- An impulse has a value of the desired peak amplitude at the desired latency and a value of zero at all other time points. This can be used to assess the impulse response function of a filter.

Note that changing the peak amplitude parameter for your function will also automatically adjust the dimensions of the Y axis in the display window.

## Basic Information for Simulation
In the middle right of the GUI you will find a section labeled “Basic Information for Simulation”. This section allows you to configure the epoch length, and select the sampling rate (Hz) or sampling period (ms). When you choose one option for sampling, the other option will be grayed out, and it will automatically adjust based on your input. For example, if you set the sampling rate to 1000 Hz, the sampling period will automatically adjust to 1 ms. If you set the sampling period to 2 ms, the sampling rate will automatically adjust to 500 Hz. Note that changing the epoch length will cause the dimensions of the X axis to change accordingly in the display window.  

Note that the sampling rate/period influences the actual epoch length. For example, if you select an epoch of -200 to +800 ms, and your sampling rate is 256 Hz, there will not be sample points at exactly -200 and +800 ms. The routine will adjust the actual start and end of the epoch to be as close as possible to the start and end times you request. A message will appear at the bottom of the GUI to notify you when this occurs.

If you have chosen to load an ERPset by selecting the “Compare with real ERP'' option, the epoch and sampling rate/period will be automatically selected to match the parameters of your loaded data, and this section will be grayed out. Once you have created a waveform that matches the loaded data, you can change the epoch and/or sampling rate/period by unselecting the “Compare with real ERP” option.

## Adding Noise to the Simulation
In the bottom right of the GUI you will find a section labeled “Add Noise to Simulation”. This section will allow you to add sinusoidal noise, white noise, and/or pink noise to your artificial ERP waveform. There is a button at the bottom of the section “Re-Randomize Noise” which will re-randomize the noise using a different seed (to learn more about seeds, [click here](https://github.com/lucklab/erplab/wiki/Using-Seeds-to-Control-Randomization-in-ERPLAB)). Note that for sinusoidal noise, the input for µV is peak amplitude, whereas for white noise and pink noise, the input is the standard deviation of a µV distribution. If you would like more control over the seeds that are used to generate noise, you can save your simulated ERP and add noise using ERPLAB -> ERP Operations -> [ERP Channel Operations](https://github.com/lucklab/erplab/wiki/EEG-and-ERP-Channel-Operations#example-of-adding-simulated-noise). Below is a picture of an artificial waveform created using an ex-gaussian function with added noise:

![Screen Shot 2023-05-22 at 1 07 08 PM](https://github.com/lucklab/erplab/assets/97117923/a7d849ef-24f1-45e4-afe1-b3725f39a867)

## Comparing Artificial Waveform with a Real ERP
In the top right corner of the GUI, there is a section labeled “Real ERP”. Within this section, you have the option to load a single ERPset, which will be superimposed on your artificial waveform for comparison. Please note that the ERPset must already be loaded into ERPLAB for this option to be accessible.

When loading an ERPset, you must select a single channel and bin to display. The “Basic Information for Simulation” will automatically adjust its settings to match the parameters of the uploaded ERPset. Additionally, the display window axes will be modified to accommodate the real ERPset. Below is a screenshot showing what it looks like:

![Screen Shot 2023-05-22 at 1 11 10 PM](https://github.com/lucklab/erplab/assets/97117923/6d648ea4-71f2-4eec-ae2b-f2188510a840)

Once you are ready to save your artificial ERP waveform, click “Create” which can be found at the bottom right of the GUI. Another GUI will pop up and give you options for naming and saving the ERPset. Once created, your artificial ERP waveform will have all the functionality of a real ERPset (note that any superimposed real ERPset will not be saved). 





