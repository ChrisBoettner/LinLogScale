# LinLogScale

This repository provides a custom symmetrical linear-logarithmic (`linlog`) scale for Matplotlib, inspired by the symlog scale. The scale is logarithmic up a a certain threshold value, after which it becomes linear.

## Features

1. **Custom Symmetrical Log Transformation**: Provides both forward and inverse transformations.
2. **Formatter for Log-Linear Scales**: Suitable for data that transitions between log and linear scales.
3. **Custom Locator**: Combines both logarithmic and linear scales.
4. **Integration with Matplotlib**: Can be easily incorporated into Matplotlib plots.

## Installation

1. Simply download and import the provided Python file into your project.
2. Ensure you have Matplotlib and numpy installed.

## Example Usage

After importing the module, you need to **register** the scale before applying the symmetrical linear-log scale to your Matplotlib plots:

```
# Assuming the library code is saved as 'linlogscale.py'
import numpy as np
import matplotlib.pyplot as plt
from matplotlib.scale import register_scale
from linlogscale import LinLogScale

# Register Scale
register_scale(LinLogScale)

# Create synthetic data
x = np.linspace(0.01, 10, 100)
y = x**2

# Create a figure and axis
fig, ax = plt.subplots()

# Apply our custom scale to the y-axis
linthresh = 10
ax.set_yscale("linlog", linthresh=linthresh, linscale=1)
ax.plot(x, y, label="y = x^2")

# Add a horizontal line to indicate the linthresh value
ax.axhline(linthresh, color="r", linestyle="--", label=f"linthresh={linthresh}")

# Display the plot
plt.legend()
plt.show()
```

