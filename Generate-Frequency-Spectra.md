## Generate Frequency Spectra

ERPLAB can return the output of a Fourier Transform (like FFT). This can be useful for examining the frequencies that make up the EEG signal, and show if there are undue artifacts, like 50 / 60 Hz electrical line noise.

### Use case 1: Quick plot
You want to quickly look at frequency spectra to visually inspect that there's nothing too awry in frequency space.

Action:
```
    [fft1, freq_labels] = compute_fourier(EEG);
    plot_fourier(fft1, freq_labels, 3, 61)
```

Result:
This will compute the Fourier Transform of data in the loaded EEG dataset, and output the frequency amplitudes in 'fft1'. The label vector, 'freq_labels', gives the identity of each element. The function 'plot_fourier' takes in 'fft1' and 'freq_labels'. The plot will be constrained between 3 Hz and 61 Hz.


### Use case 2: Save FFT to text file

```
[fft2, freq_labels] = compute_fourier(EEG);
fft_csv = [freq_labels', fft2'];
csvwrite('test_fft.csv',fft_csv);
```

Result:
This will compute the fourier transform, and write the output to text file called 'test_fft.csv'. The first column will be the frequency labels, and the second column will be the amplitude spectra.

### Use case 3: Single channel, downsampled FFT

```
chan_here = 3;
smooth_factor = 2;
[fft3, freq_labels] = compute_fourier(EEG,chan_here,smooth_factor);
```

Result:
This will run the FFT on only channel 3 of the given EEG dataset. Additionally, the 'smooth_factor' is used to downsample the FFT, so that x/2 points are returned. Thus, the output is half as long. The elements are averaged together, so there are half as many frequency bins, each with twice the width.

See also:
```
help compute_fourier
help plot_fourier
