---
layout: post
title: "Testing Hydrology Code and Math Formulas"
date: 2026-07-28
categories: [Research, Tech]
tags: [python, hydrology]
---

Hello! This post serves as a test to see how my blog engine renders scientific text, programming code, and math equations.

## 🐍 Python Code Snippet

Here is a quick Python script using pandas to calculate average monthly rainfall data. Because we specified `highlighter: rouge` in our configuration, the keywords and strings below will be beautifully colored on the live website.

```python
import pandas as pd

# Load climate observation data
data = {'Month': ['Jan', 'Feb', 'Mar'], 'Rainfall_mm': [45.2, 58.1, 72.0]}
df = pd.DataFrame(data)

# Calculate the mean monthly rainfall
mean_rain = df['Rainfall_mm'].mean()
print(f"Average Rainfall: {mean_rain:.2f} mm")
```

## 📐 Hydrology Equation

Thanks to `markdown: kramdown`, we can write standard mathematical equations using LaTeX syntax. Below is the fundamental water balance equation:

$$ P = Q + E + \Delta S $$

Where:
* **$P$** is Precipitation
* **$Q$** is Runoff
* **$E$** is Evapotranspiration
* **$\Delta S$** is the Change in Water Storage

---
Everything looks correct! Let me know if you are ready to publish this to your live site.
