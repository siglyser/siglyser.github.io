# SigLyser

**SigLyser** is a Python library for analysing vibration signals from rotating machinery. It provides frequency-domain transformations and statistical measures built on NumPy and SciPy.

## Features

- **FFT** — single-sided amplitude spectrum from time-domain data
- **3D FFT** — speed-frequency amplitude map (waterfall) segmented by engine cycle
- **RMS & Amplitude** — root mean square and peak-to-peak amplitude per cycle vs speed

## Quick example

```python
import numpy as np
from siglyser import calc_fft

t = np.linspace(0, 1, 1000)
signal = np.sin(2 * np.pi * 50 * t)

freq, amp = calc_fft(t, signal)
```

## Installation

```bash
pip install siglyser
```

## Links

- [Source code](https://github.com/siglyser/siglyser)
- [PyPI](https://pypi.org/project/siglyser/)
- [Issue tracker](https://github.com/siglyser/siglyser/issues)
