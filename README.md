# Comparative Analysis of Stereo Matching Pipelines

**Authors:** Wenye Xiong, Xinyue Wang, Meihan Zheng  
**Course:** ES143 Computer Vision, Harvard University

## Overview

This project implements and evaluates a complete stereo vision pipeline, ranging from hardware calibration to dense disparity estimation. We present a comparative analysis of three distinct approaches to stereo matching:

1. **Local Methods:** Winner-Take-All (WTA) strategies with Sum of Absolute Differences (SAD) and Census Transform.
2. **Global Optimization:** Scanline Dynamic Programming (DP).
3. **Deep Learning:** State-of-the-art RAFT-Stereo architecture and Semi-Global Block Matching (SGBM).

The project utilizes data captured from a custom-calibrated dual-smartphone rig and a mirror-based single-camera setup.

## Repository Contents

* **`calibration.ipynb`**: Handles camera calibration and image rectification. It utilizes the `pupil-apriltags` library to detect AprilTags, calculates camera intrinsics/extrinsics, and generates rectified stereo pairs.
* **`Stereo.ipynb`**: The main experimentation notebook. It implements the stereo matching algorithms (SAD, Scanline DP, RAFT-Stereo), loads rectified images, and visualizes disparity maps.
* **`Wenye_Xiong_Meihan_Zheng_Xinyue_Wang_Final.pdf`**: Final project report detailing theoretical background, hardware setup, methodology, and results.

## ⚠️ Important: Running on Google Colab

These notebooks are designed to be run in **Google Colab** with data stored in **Google Drive**.

### 1. Directory Setup
**Crucial Step:** You must configure the working directory to match your specific Google Drive path.

1. Mount your Google Drive in the notebook.
2. Locate the `PROJECT_DIR` variable in the code (usually near the top).
3. **Update the path** to point to the folder where you saved this repository.

*Example from `Stereo.ipynb`:*
```python
from google.colab import drive
drive.mount('/content/drive')

import os
# CHANGE THIS PATH to your actual folder location
PROJECT_DIR = "/content/drive/MyDrive/es-143-assignments-group/Final" 
os.chdir(PROJECT_DIR)
```

### 2. Dependencies
To install the required AprilTag detector for calibration, run the following command in a code cell:

```python
%pip install pupil-apriltags
```

## Usage Workflow

### Step 1: Calibration (calibration.ipynb)
Run this notebook first to generate the necessary data for stereo matching.

- **Input:** Raw images (e.g., from `./data_mirror/left_half`).
- **Process:** Detects tags, computes geometry, and rectifies images.
- **Output:** Saves processed images to the `rectified_images_output` directory.

### Step 2: Stereo Matching (Stereo.ipynb)
Run this notebook after calibration is complete.

- **Input:** Rectified images from `rectified_images_output`.
- **Process:**
    - WTA + SAD: Local cost matching.
    - Dynamic Programming: Global optimization for occlusion handling.
    - SGBM: Semi-global block matching.
    - RAFT-Stereo: Deep learning inference (requires model weights).
- **Output:** Disparity maps and visualizations.

## Results

Our experiments show that while RAFT-Stereo provides superior robustness in textureless regions, global optimization techniques like Dynamic Programming offer effective handling of occlusions compared to simple local methods. Detailed quantitative results can be found in the accompanying PDF report.
