# Quickstart

This page walks through the three main analysis workflows in SigLyser.

## 1. FFT of a time-domain signal

Use `calc_fft` when you have a vibration signal recorded at (approximately) uniform intervals and want its frequency spectrum.

```python
import numpy as np
import matplotlib.pyplot as plt
from siglyser import calc_fft

# --- load your data ---
# time_sec: 1-D array of time stamps in seconds
# vibr:     1-D array of vibration values (e.g. acceleration in g)

freq, amp = calc_fft(time_sec, vibr)

plt.plot(freq, amp)
plt.xlabel("Frequency (Hz)")
plt.ylabel("Amplitude")
plt.title("FFT")
plt.show()
```

## 2. Speed-frequency map (3D FFT / waterfall)

Use `calc_3dfft` when you also have a simultaneous speed trace (RPM). The function segments the signal by engine cycle and produces a 2-D amplitude grid suitable for a contour or surface plot.

```python
from siglyser import calc_3dfft, plot_3dfft
import matplotlib.pyplot as plt

# time_sec, speed_rpm, vibr — all same-length 1-D arrays

freq_x, speed_y, amp_z = calc_3dfft(time_sec, speed_rpm, vibr)

plot_3dfft(freq_x, speed_y, amp_z, xlim=(0, 1000), ylim=(500, 6000))
plt.xlabel("Frequency (Hz)")
plt.ylabel("Speed (RPM)")
plt.title("3D FFT — Speed vs Frequency")
plt.show()
```

## 3. RMS and amplitude vs speed

Use `calc_rms_ampl` to track overall vibration level through a speed sweep (run-up or run-down).

```python
from siglyser import calc_rms_ampl
import matplotlib.pyplot as plt

speed, rms, amplitude = calc_rms_ampl(time_sec, speed_rpm, vibr)

plt.plot(speed, rms, label="RMS")
plt.plot(speed, amplitude, label="Amplitude (half peak-to-peak)")
plt.xlabel("Speed (RPM)")
plt.ylabel("Vibration")
plt.legend()
plt.show()
```

## Input data format

All functions expect **1-D NumPy arrays** (or any array-like that NumPy can convert). Ensure:

- `time_sec`, `speed_rpm`, and `vibr` are the **same length**
- `time_sec` values are **monotonically increasing**
- `speed_rpm` values are **positive** (the functions assume a rotating system)
