# Video Presentation Script - Lane Detection Assignment

## Overview
- **Duration:** 4 minutes
- **Team Size:** 5 members
- **Format:** Screen recording with notebook demo

---

## Time Distribution

| Time | Member | Topic | Duration |
|------|--------|-------|----------|
| 0:00 - 0:45 | Member 1 | Introduction & Problem Statement | 45 sec |
| 0:45 - 1:30 | Member 2 | Preprocessing (Grayscale, Blur, Canny) | 45 sec |
| 1:30 - 2:15 | Member 3 | ROI & Hough Transform | 45 sec |
| 2:15 - 3:00 | Member 4 | ML Methods (Slope, RANSAC) | 45 sec |
| 3:00 - 4:00 | Member 5 | Live Demo & Results | 60 sec |

---

## Member 1: Introduction (0:00 - 0:45)

**What to show:** Notebook title cell or a simple title slide

**Script:**

"Hi everyone, we are Group [YOUR GROUP NUMBER] presenting our lane detection assignment for Computer Vision course.

The problem we're solving is: detecting lane lines on road images using classical computer vision techniques - without using any deep learning.

Our approach has 5 main steps:
1. Preprocess the image - convert to grayscale and reduce noise
2. Detect edges using the Canny algorithm
3. Apply a region of interest mask to focus on the road
4. Find line segments using Hough Transform
5. Use machine learning techniques to fit the final lane lines

Now I'll hand over to [Member 2 name] who will explain the preprocessing steps."

---

## Member 2: Preprocessing (0:45 - 1:30)

**What to show:** Run cells 4-9 showing the preprocessing steps

**Script:**

"Thanks. Let me explain how we preprocess the image.

[Run the cell to show original image]

Step 1 is converting to grayscale. Color information doesn't really help us detect lanes, and grayscale is much simpler to work with - just one channel instead of three.

Step 2 is applying Gaussian blur with a 5x5 kernel. This smooths out small noise in the image. Without this step, edge detection would pick up too much noise and give us false edges.

Step 3 is Canny edge detection. This algorithm finds pixels where the intensity changes sharply - which is exactly what lane markings look like.

[Point to the output]

We use thresholds of 50 and 150. The 3:1 ratio is a standard recommendation for Canny. Pixels with gradient above 150 are definitely edges, below 50 are definitely not edges.

You can see in the output that the lane lines show up clearly as white edges.

Now [Member 3 name] will explain how we focus on just the road area."

---

## Member 3: ROI & Hough Transform (1:30 - 2:15)

**What to show:** Run cells 10-13 showing ROI mask and Hough lines

**Script:**

"Thanks. So we have edge pixels now, but there's a lot of stuff we don't care about - edges from trees, the sky, other vehicles.

[Show the ROI visualization]

We create a Region of Interest mask - basically a trapezoid shape that covers only the road area in front of the car. Everything outside this region gets masked out.

Now for the key algorithm - Hough Transform.

The mathematical idea is that any line can be represented as:
rho equals x times cosine theta plus y times sine theta

For each edge pixel, we calculate all possible rho-theta pairs. Where many pixels agree on the same parameters, we have detected a line.

[Show Hough output]

OpenCV's HoughLinesP function gives us line segments directly. We found [X] segments in this image.

The parameters we tuned:
- Threshold of 30 votes minimum
- Minimum line length of 40 pixels
- Maximum gap of 100 pixels to connect broken lines

[Member 4 name] will now explain how we separate these into left and right lanes."

---

## Member 4: ML Methods (2:15 - 3:00)

**What to show:** Run cells 14-18 showing classification and fitting

**Script:**

"Thanks. We have multiple line segments, but we need to figure out which belong to the left lane and which to the right.

[Show the slope classification output]

The key insight is about slope. In image coordinates where y increases downward:
- Left lane lines go from bottom-left to top-right, so they have NEGATIVE slope
- Right lane lines go from bottom-right to top-left, so they have POSITIVE slope

We discard any lines with slope close to zero - those are horizontal and not lane markings.

Now we have multiple segments per lane but need just ONE final line. We tried three ML approaches:

1. Simple Averaging - just take the mean slope and intercept. Fast but sensitive to outliers.

2. RANSAC - Random Sample Consensus. This randomly samples points, fits lines, and keeps the one with most inliers. It's robust to outliers.

3. K-Means clustering in slope-intercept space.

[Show the comparison visualization]

All three give similar results on clean images. We chose RANSAC because it handles noisy data better.

[Member 5 name] will now show the complete demo."

---

## Member 5: Demo & Results (3:00 - 4:00)

**What to show:** Run the complete pipeline on all images

**Script:**

"Let me run our complete pipeline on all test images.

[Run the detect_lanes cell]

[Wait for output to appear]

As you can see, the system successfully detects both lane lines on all our test images. The blue line is the left lane, green is the right lane, and the green shaded area shows the detected lane region.

Let me show the statistics:

[Run the stats cell]

For each image we're detecting around [X] line segments, classifying them correctly into left and right, and fitting clean final lines.

Some limitations we observed:
- The system assumes straight lanes, so curved roads don't work well
- Strong shadows can create false edges
- If lane markings are faded, detection might fail

For future improvement, we could:
- Use polynomial fitting instead of straight lines for curves
- Add color filtering to specifically look for white and yellow
- Apply temporal smoothing if processing video

That concludes our presentation. The code is available in our GitHub repository. Thank you for watching!"

---

## Recording Tips

### Before Recording:
1. Open the notebook in VS Code
2. Make sure the kernel is selected and working
3. Clear all outputs (so you can run fresh)
4. Practice your part once
5. Keep the script nearby but don't read word-for-word

### During Recording:
1. Share your screen showing VS Code
2. Run cells as you explain (more engaging than static slides)
3. Point to specific parts of the output
4. Speak clearly and at moderate pace
5. It's okay to pause briefly between sections

### Tools for Recording:
- **Zoom:** Start a meeting alone, share screen, record
- **OBS Studio:** Free, professional quality
- **QuickTime (Mac):** File > New Screen Recording
- **Loom:** Easy to use, free tier available
- **Microsoft Teams:** Similar to Zoom

### After Recording:
1. Watch it once to check audio/video quality
2. Trim any long pauses if needed
3. Export as MP4
4. Check file size (compress if too large)

---

## Cells to Run During Demo

For smooth demo, run these cells in order:

1. **Cell 4:** Import libraries
2. **Cell 6:** Load images
3. **Cell 7:** Display original images
4. **Cell 9:** Show preprocessing steps
5. **Cell 11:** Show ROI mask
6. **Cell 13:** Show Hough lines
7. **Cell 15:** Show slope classification
8. **Cell 18:** Compare fitting methods
9. **Cell 20:** Run complete pipeline on all images
10. **Cell 22:** Show statistics

---

## Quick Reference - Key Points to Mention

### Algorithms Used:
- Gaussian Blur (noise reduction)
- Canny Edge Detection (find edges)
- Hough Transform (detect lines)
- RANSAC (robust line fitting)

### Parameters:
- Blur kernel: 5x5
- Canny thresholds: 50, 150
- Hough threshold: 30
- Min line length: 40px
- Max line gap: 100px
- Slope threshold: 0.3

### Math Formula:
- Hough Transform: ρ = x·cos(θ) + y·sin(θ)
- Slope: m = (y2 - y1) / (x2 - x1)

---

Good luck with the recording! 🎬
