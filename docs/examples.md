# Examples

## Synthetic sine wave — verifying FFT

A pure sine wave at a known frequency is a good sanity check for `calc_fft`.

```python
import numpy as np
import matplotlib.pyplot as plt
from siglyser import calc_fft

fs = 5000          # sampling rate (Hz)
duration = 1.0     # seconds
f0 = 200           # frequency of test tone (Hz)

t = np.arange(0, duration, 1 / fs)
signal = np.sin(2 * np.pi * f0 * t)

freq, amp = calc_fft(t, signal)

plt.figure(figsize=(8, 4))
plt.plot(freq, amp)
plt.axvline(f0, color="red", linestyle="--", label=f"Expected peak at {f0} Hz")
plt.xlabel("Frequency (Hz)")
plt.ylabel("Amplitude")
plt.xlim(0, 500)
plt.legend()
plt.tight_layout()
plt.show()
```

Expected output: a single peak at 200 Hz.

---

## Engine run-up — waterfall plot

This example simulates an engine accelerating from 1 000 to 5 000 RPM.

```python
import numpy as np
import matplotlib.pyplot as plt
from siglyser import calc_3dfft, plot_3dfft

fs = 5000
duration = 30.0
t = np.arange(0, duration, 1 / fs)

# linearly increasing speed
rpm = np.linspace(1000, 5000, len(t))

# fundamental firing frequency (4-cylinder 4-stroke: 2 firings per revolution)
firing_freq = (rpm / 60) * 2
signal = np.sin(2 * np.pi * np.cumsum(firing_freq / fs))

freq_x, speed_y, amp_z = calc_3dfft(t, rpm, signal)

plt.figure(figsize=(10, 6))
plot_3dfft(freq_x, speed_y, amp_z, xlim=(0, 300), ylim=(1000, 5000))
plt.xlabel("Frequency (Hz)")
plt.ylabel("Speed (RPM)")
plt.title("Engine Run-up Waterfall")
plt.tight_layout()
plt.show()
```

---

## RMS and amplitude through a speed sweep

```python
import numpy as np
import matplotlib.pyplot as plt
from siglyser import calc_rms_ampl

fs = 5000
duration = 20.0
t = np.arange(0, duration, 1 / fs)

rpm = np.linspace(1000, 4000, len(t))
firing_freq = (rpm / 60) * 2
signal = 0.5 * np.sin(2 * np.pi * np.cumsum(firing_freq / fs))

speed, rms, amplitude = calc_rms_ampl(t, rpm, signal)

plt.figure(figsize=(8, 4))
plt.plot(speed, rms, label="RMS")
plt.plot(speed, amplitude, label="Amplitude")
plt.xlabel("Speed (RPM)")
plt.ylabel("Vibration (g)")
plt.legend()
plt.tight_layout()
plt.show()
```
