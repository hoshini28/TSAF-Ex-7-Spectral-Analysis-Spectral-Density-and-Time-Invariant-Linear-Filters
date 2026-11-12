# TSAF-Ex-7-Spectral-Analysis-Spectral-Density-and-Time-Invariant-Linear-Filters

## AIM:

To simulate a time series, calculate its spectral density, perform spectral analysis using
the periodogram, and study the effect of a time-invariant linear filter.

## PROGRAM:

```
import numpy as np
import matplotlib.pyplot as plt
from scipy import signal

# 1. Setup time array
n = 500
t = np.arange(n)

# 2. Time series with two close frequencies (0.08 and 0.18) + Noise
x = np.sin(2 * np.pi * 0.08 * t) + 0.7 * np.sin(2 * np.pi * 0.18 * t) + 0.3 * np.random.randn(n)

# 3. Dominant frequency search
f_raw, p_raw = signal.periodogram(x)
print("Top Peak Frequency:", f_raw[np.argmax(p_raw)])

# 4. Create Weighted Exponential Kernel
window_size = 9
weights = np.exp(-np.linspace(-2, 2, window_size)**2)
kernel = weights / np.sum(weights) # Normalize weights
filtered = np.convolve(x, kernel, mode="same")

# 5. Compute Spectrums
f_filt, p_filt = signal.periodogram(filtered)

# 6. Plotting
plt.figure(figsize=(10, 6))
plt.subplot(2, 1, 1)
plt.plot(t, x, label="Original", alpha=0.5)
plt.plot(t, filtered, label="Gaussian Weighted Filtered", color='green')
plt.title("Original vs Exponentially Weighted Filtered Series")
plt.legend()
plt.subplot(2, 1, 2)
plt.plot(f_raw, p_raw, label="Original Density", alpha=0.6)
plt.plot(f_filt, p_filt, label="Gaussian Filtered Density", color='green')
plt.title("Spectral Power Comparison")
plt.legend()
plt.tight_layout()
plt.show()

```

## OUTPUT:

<img width="690" height="445" alt="image" src="https://github.com/user-attachments/assets/5d90c9d4-1d48-4235-9864-f045c3875f05" />
