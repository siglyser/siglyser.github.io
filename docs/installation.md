# Installation

## Requirements

- Python 3.8 or later
- NumPy
- SciPy
- Matplotlib

## Install from PyPI

```bash
pip install siglyser
```

## Install from source

```bash
git clone https://github.com/siglyser/siglyser.git
cd siglyser
pip install .
```

## Verify the installation

```python
import siglyser
print(dir(siglyser))
# ['calc_3dfft', 'calc_fft', 'calc_rms_ampl', 'plot_3dfft']
```
