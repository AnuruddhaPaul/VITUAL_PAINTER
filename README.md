# AI Virtual Painter

![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)

AI Virtual Painter is a computer vision-based system that allows users to draw on a virtual canvas using hand gestures captured by a webcam. This project leverages **MediaPipe** for hand tracking and **OpenCV** for image processing and visualization.

---

## Table of Contents

- [Overview](#overview)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [Gesture Controls](#gesture-controls)
- [Code Explanation](#code-explanation)
- [Customization](#customization)
- [Troubleshooting](#troubleshooting)
- [License](#license)

---

## Overview

This project implements a virtual painting canvas controlled by hand gestures. Using your webcam, you can:

- **Draw on a virtual canvas** by moving your index finger.
- **Select different colors** from a menu at the top of the screen.
- **Erase parts of your drawing** by selecting the eraser tool.
- **Exit the program** by pressing the `q` key.

---

## Requirements

Ensure you have the following installed:

- Python 3.6+
- OpenCV
- NumPy
- MediaPipe
- A working webcam

---

## Installation

Clone this repository:

```bash
git clone https://github.com/yourusername/ai-virtual-painter.git
cd ai-virtual-painter
```

Install the required dependencies:

```bash
pip install opencv-python numpy mediapipe
```

---

## Usage

Run the main script:

```bash
python VIRTUAL_PAINTER.py
```

---

## Gesture Controls

| Gesture | Action |
|-----------------|------------------------|
| Index finger up | Drawing mode |
| Index + Middle fingers up | Selection mode |
| Point to color menu with two fingers | Select color/eraser |
| Press 'q' key | Exit program |

---

## Code Explanation

### `VIRTUAL_PAINTER.py`

This script contains the main logic for hand gesture-based painting.

- **Initialization and Setup:**
```python
brushThickness = 15
eraserThickness = 100
imgCanvas = np.zeros((720, 1280, 3), np.uint8)
```
- Defines brush and eraser thickness.
- Creates a blank canvas for drawing.

- **Main Loop Features:**

- **Hand Detection:**
```python
img = detector.findHands(img)
lmList, _ = detector.findPosition(img, draw=False)
```
- **Mode Selection:**
```python
if fingers[1] and fingers[2]:
    print("Selection Mode")
    # Color selection logic
```
- **Drawing:**
```python
if fingers[1] and fingers[2] == False:
    cv2.circle(img, (x1, y1), 15, drawColor, cv2.FILLED)
    print("Drawing Mode")
    # Drawing logic
```

### `HAND_TRACKING_MODULE.py`

This module provides a reusable class for detecting and tracking hand movements.

- **Hand Detection:**
```python
def findHands(self, img, draw=True):
    imgRGB = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
    self.results = self.hands.process(imgRGB)
    return img
```
- **Finger Tracking:**
```python
def fingersUp(self):
    fingers = []
    # Checks which fingers are extended
    return fingers
```

---

## Customization

You can adjust parameters to personalize your experience:

- **Brush Settings:**
```python
brushThickness = 15  # Adjust brush thickness
eraserThickness = 100  # Adjust eraser thickness
```
- **Camera Resolution:**
```python
cap.set(3, 1680)  # Width
cap.set(4, 820)   # Height
```
- **Colors:**
Modify the color palette by changing the RGB values in the `drawColor` variable.

---

## Troubleshooting

| Issue | Solution |
|------------------------|-----------------------------------------------|
| Poor detection | Ensure good lighting and a clear background |
| Drawing not appearing | Check that your index finger is properly tracked |
| Colors not selecting | Make sure both index and middle fingers are detected in selection mode |
| No detection | Check webcam functionality |
| Performance issues | Lower camera resolution or brush thickness |

---

## License

This project is licensed under the MIT License.

---

_Last updated: March 17, 2025_
