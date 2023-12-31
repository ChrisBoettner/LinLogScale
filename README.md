# LinLogScale

This repository provides a custom linear-logarithmic (`linlog`) scale for Matplotlib, inspired by the symlog scale. The scale is logarithmic up a a certain threshold value, after which it becomes linear.

## Features

1. **Custom LinLog Transformation**: Provides both forward and inverse transformations.
2. **Formatter for Log-Linear Scales**: Suitable for data that transitions between log and linear scales.
3. **Custom Locator**: Combines both logarithmic and linear scales.
4. **Integration with Matplotlib**: Can be easily incorporated into Matplotlib plots.

## Installation

1. Simply download and import the provided Python file into your project.
2. Ensure you have Matplotlib and numpy installed.

## Usage and Example

After importing the module, you need to **register the scale** before applying the linear-log scale to your Matplotlib plots:

```
# Assuming the library code is saved as 'linlogscale.py'
from matplotlib.scale import register_scale
from linlogscale import LinLogScale

# Register Scale
register_scale(LinLogScale)
```

The scale can then be applied to any plot using the `ax.set_yscale` command.

```
import numpy as np
import matplotlib.pyplot as plt

# Create synthetic data
x = np.linspace(0.01, 10, 100)
y = x**2

# Create a figure and axis
fig, ax = plt.subplots()

# Apply the linlog scale to the y-axis
linthresh = 10

ax.set_yscale("linlog", base=10, linthresh=linthresh, linscale=1, clip_value = "mask")

# Plot the data and display the plot
ax.plot(x, y, label="y = x^2")

ax.axhline(linthresh,  color="r", linestyle="--", label=f"linthresh={linthresh}")

plt.legend()
plt.show()
```

The behaviour for inputs <=0 can be set using clip_value. The default is ```"mask"```, which effectively masks out these values. However, clip_value can be set, so that all inputs <=0 will be set to this value.

Specifically, this is needed when making **bar plots**, with bars starting at 0. In this case,  **clip_value should be set to some value smaller than the lowest bar height**. For example:

```
x = [1, 2 , 3, 4, 5]
y = [2, 0.1, 0.003, 3, 0.7]

fig, ax = plt.subplots()

linthresh = 1
clip_value = 0.0001

ax.set_yscale("linlog", base=10, linthresh=linthresh, linscale=1, clip_value = clip_value)
ax.set_ylim(clip_value, 1.2*max(y))

ax.bar(x, y)

ax.axhline(linthresh, color="r")

plt.show()
```
