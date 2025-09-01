---
layout: default
title: "AFM Data Analysis Guide"
---

# AFM Data Analysis with ImageJ

## Overview

This guide walks you through analyzing Atomic Force Microscopy (AFM) data using ImageJ software. You'll learn to process raw AFM images, extract quantitative measurements, and create publication-quality figures.

## Prerequisites

- ImageJ software installed ([Download here](https://imagej.nih.gov/ij/download.html))
- Basic understanding of AFM principles
- AFM data files (.spm, .tiff, or similar formats)

---

## Step 1: Import AFM Data

### For .spm Files:
1. Open ImageJ
2. Go to **File → Import → Raw...**
3. Select your AFM data file
4. Set parameters:
   - **Image type**: 32-bit Real
   - **Width**: Check your AFM software specifications
   - **Height**: Match the width for square images
   - **Number of images**: Usually 1 for topography

### For Other Formats:
- **TIFF files**: Use **File → Open**
- **Gwyddion files**: Export as TIFF from Gwyddion first

---

## Step 2: Basic Image Processing

### 2.1 Flatten the Image
Remove sample tilt and scanner drift:

1. **Process → Filters → Subtract Background**
2. Set **Rolling ball radius**: 50-100 pixels
3. Check **Sliding paraboloid** for better results

### 2.2 Apply Filters
Reduce noise while preserving features:

1. **Process → Filters → Gaussian Blur**
2. Set **Sigma**: 0.5-1.0 pixels (start small)
3. For line noise: **Process → FFT → Bandpass Filter**

---

## Step 3: Measurements and Analysis

### 3.1 Height Measurements
1. Use **Line** tool to draw across features
2. **Analyze → Plot Profile**
3. Measure peak-to-valley distances
4. Save data: **Data → Save As...**

### 3.2 Surface Roughness
1. **Analyze → Set Measurements** → Check **Mean**, **StdDev**
2. Select region with **Rectangle** tool
3. **Analyze → Measure**
4. Standard deviation = RMS roughness

### 3.3 Particle Analysis
1. **Image → Adjust → Threshold**
2. Set threshold to highlight particles
3. **Analyze → Analyze Particles**
4. Set size filters and circularity

---

## Step 4: Creating Publication Figures

### 4.1 Scale Bar
1. **Analyze → Tools → Scale Bar**
2. Set appropriate length (e.g., 1 μm)
3. Choose position and styling

### 4.2 Color Scale
1. **Image → Lookup Tables** → Choose appropriate LUT
2. **Analyze → Tools → Calibration Bar**
3. Position and format as needed

### 4.3 Export High-Quality Images
1. **File → Save As → TIFF**
2. For publications: Set to 300 DPI minimum
3. **Image → Scale** → Increase size if needed

---

## Troubleshooting

### Common Issues:

**Streaky/noisy images:**
- Try median filter: **Process → Filters → Median** (radius 1-2)
- Check AFM tip condition

**Drift or tilt:**
- Use **Process → Subtract Background** with larger rolling ball
- Manual correction: **Process → Math → Subtract** with fitted plane

**Poor contrast:**
- **Image → Adjust → Brightness/Contrast**
- **Process → Enhance Contrast** (0.1% saturated)

---

## Advanced Tips

1. **Batch Processing**: Use **Process → Batch** for multiple files
2. **Macros**: Record repetitive tasks with **Plugins → Macros → Record**
3. **3D Visualization**: **Plugins → 3D → 3D Viewer**
4. **Line Profile Analysis**: **Plugins → Plot → Profile Plot Tools**

---

## Quick Reference Tables

### Common ImageJ Filters

| Filter Type | Purpose | Settings | When to Use |
|-------------|---------|----------|-------------|
| Gaussian Blur | Noise reduction | Sigma: 0.5-1.0 | Light noise, preserve edges |
| Median | Remove outliers | Radius: 1-2 | Salt-and-pepper noise |
| Bandpass Filter | Remove periodic noise | Low: 3, High: 40 | Line/scan artifacts |
| Subtract Background | Remove tilt/drift | Rolling ball: 50-100 | Sample tilt, scanner drift |

### Typical AFM Parameters

| Parameter | Tapping Mode | Contact Mode | Units |
|-----------|--------------|--------------|-------|
| Scan Rate | 0.5-2.0 | 0.1-1.0 | Hz |
| Resolution | 512x512 | 256x256 | pixels |
| Set Point | 70-90% | N/A | % of free amplitude |

---

<!-- 
## Video Tutorials

### Embedding YouTube Videos
For step-by-step visual guidance, check out these tutorials:

**ImageJ Basics for AFM:**
<iframe width="560" height="315" src="https://www.youtube.com/embed/dQw4w9WgXcQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

**Advanced AFM Analysis:**
- [ImageJ Line Profile Analysis](https://www.youtube.com/watch?v=example1)
- [3D Surface Visualization](https://www.youtube.com/watch?v=example2)
-->

---

## Code Examples

### ImageJ Macro Example
```javascript
// Batch process AFM images
dir = getDirectory("Choose a Directory");
list = getFileList(dir);

for (i=0; i<list.length; i++) {
    if (endsWith(list[i], ".tif")) {
        open(dir+list[i]);
        run("Subtract Background...", "rolling=50");
        run("Gaussian Blur...", "sigma=0.5");
        saveAs("Tiff", dir+"processed_"+list[i]);
        close();
    }
}
```

### Python Data Processing
```python
import numpy as np
import matplotlib.pyplot as plt
from scipy import ndimage

# Load AFM data
data = np.loadtxt('afm_data.txt')

# Apply Gaussian filter
filtered_data = ndimage.gaussian_filter(data, sigma=1.0)

# Calculate roughness
rms_roughness = np.std(filtered_data)
print(f"RMS Roughness: {rms_roughness:.2f} nm")
```

---

## Image Examples

### Before and After Processing

![AFM Raw Data](assets/img/placeholder/smiley.png)
*Figure 1: Raw AFM topography showing noise and tilt*

![AFM Processed](assets/img/placeholder/smiley.png)
*Figure 2: Same data after background subtraction and filtering*

---

## Markdown Formatting Reference

### Text Formatting
- **Bold text**: `**Bold text**`
- *Italic text*: `*Italic text*`
- `Code text`: `` `Code text` ``
- ~~Strikethrough~~: `~~Strikethrough~~`

### Lists
**Numbered List:**
1. First item
2. Second item
3. Third item

**Bullet List:**
- First item
- Second item
- Third item

### Links and References
- [External link](https://example.com)
- [Internal page link](../student-resources)
- [Email link](mailto:fernando@union.edu)

### Blockquotes
> **Important Note:** Always backup your original AFM data before processing. ImageJ operations can be destructive if not used carefully.

### Alert Boxes
⚠️ **Warning:** High voltage components - ensure proper safety training before use.

✅ **Tip:** Save intermediate processing steps to track your workflow.

📝 **Note:** Contact lab members if you encounter unusual artifacts in your data.

---

## Resources

- [ImageJ User Guide](https://imagej.nih.gov/ij/docs/guide/)
- [AFM Image Analysis Tutorial](https://www.youtube.com/watch?v=example)
- Lab SOPs: Contact Dr. Fernando for detailed protocols

---

**Questions?** Contact lab members or attend the weekly ImageJ training session (Fridays 2 PM, Lab 204).

**Last Updated**: August 2024