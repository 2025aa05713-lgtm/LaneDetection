# Lane Line Detection Using Classical Computer Vision & Machine Learning

## Assignment 1 - Problem Statement 2
### Computer Vision (S2-25_AIMLCZG525)

---

## Overview

This project implements a robust system for detecting straight lane lines in road images using classical computer vision and machine learning techniques.

## Pipeline

```
Input Image → Grayscale → Gaussian Blur → Canny Edge Detection → ROI Mask → 
Hough Transform → Slope Classification → ML Line Fitting → Output
```

## Key Techniques

1. **Preprocessing**: Color space conversion, Gaussian blur
2. **Edge Detection**: Canny algorithm
3. **Feature Extraction**: Region of Interest (ROI) masking
4. **Line Detection**: Probabilistic Hough Transform
5. **ML Filtering**: Slope-based classification + RANSAC/K-Means/Averaging

## Project Structure

```
LaneDetection/
├── Lane_Detection_Assignment.ipynb  # Main Jupyter notebook
├── requirements.txt                  # Python dependencies
├── README.md                         # This file
├── images/                           # Test images
│   ├── road_image_1.jpg
│   ├── road_image_2.jpg
│   └── road_image_3.jpg
├── output/                           # Detection results
└── .venv/                            # Virtual environment
```

## Setup Instructions

### 1. Create Virtual Environment (if not exists)
```bash
python3 -m venv .venv
source .venv/bin/activate  # On macOS/Linux
# or
.venv\Scripts\activate     # On Windows
```

### 2. Install Dependencies
```bash
pip install -r requirements.txt
```

### 3. Register Jupyter Kernel
```bash
python -m ipykernel install --user --name=lane-detection --display-name="Python (Lane Detection)"
```

### 4. Run the Notebook
```bash
jupyter notebook Lane_Detection_Assignment.ipynb
```

## Parameters

| Parameter | Value | Description |
|-----------|-------|-------------|
| Blur Kernel | 5 | Gaussian blur kernel size |
| Canny Low | 50 | Lower threshold for edge detection |
| Canny High | 150 | Upper threshold for edge detection |
| Hough Threshold | 30 | Minimum votes for line detection |
| Min Line Length | 40 | Minimum line segment length |
| Max Line Gap | 100 | Maximum gap between segments |
| Slope Threshold | 0.3 | Minimum slope for lane classification |

## ML Methods Implemented

1. **Simple Averaging**: Mean slope and intercept
2. **RANSAC**: Robust fitting resistant to outliers
3. **K-Means**: Clustering in (slope, intercept) space

## Results

The pipeline successfully detects lane lines in various road conditions. See the `output/` folder for results.

## Limitations

- Assumes straight lanes (no curve detection)
- May struggle with shadows or poor lighting
- Requires visible lane markings

## Author

[Your Name] - [Your Student ID]

## License

This project is for educational purposes as part of the BITS Pilani Computer Vision course.
