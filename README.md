# Color Object Detection in Video Stream

This script captures video from your webcam and detects specific color objects, highlighting them with bounding boxes. It tracks two colors: **yellow** and **pink**, using OpenCV for video processing, color conversion, and contour detection.

## Features
- Converts frames to HSV color space to detect colors more effectively.
- Applies Gaussian blur to reduce noise.
- Detects objects based on defined color ranges.
- Highlights detected objects with bounding boxes.
- Supports live video feed using your webcam.
- Exits the program by pressing the `q` key.

## Prerequisites

Before running the script, make sure you have the following installed:

- Python 3.x
- OpenCV
- NumPy

You can install the required libraries using `pip`:

```bash
pip install opencv-python numpy
```

## Code Explanation

### Function: `getLimits(color)`
This function calculates the HSV color range for a given BGR color.

- Converts the BGR color to HSV.
- Returns the lower and upper HSV limits with some tolerance.

```python
def getLimits(color):
    c = np.uint8([[color]])
    hsvC = cv.cvtColor(c, cv.COLOR_BGR2HSV)

    lowerLimit = hsvC[0][0][0] - 10, 100, 100
    upperLimit = hsvC[0][0][0] + 10, 255, 255

    lowerLimit = np.array(lowerLimit, dtype=np.uint8)
    upperLimit = np.array(upperLimit, dtype=np.uint8)

    return lowerLimit, upperLimit
```

### Main Workflow
1. Capture video from the webcam using `cv.VideoCapture(0)`.
2. Apply Gaussian blur to each frame to reduce noise.
3. Convert the blurred frame from BGR to HSV color space.
4. Define the yellow and pink colors in BGR format.
5. Use `getLimits()` to get the HSV color ranges for pink and yellow.
6. Create masks to isolate the pink and yellow colors in the frame.
7. Apply morphological operations to remove noise from the mask.
8. Detect contours and draw bounding boxes around the detected objects.
9. Display the original frame with bounding boxes and the mask.
10. Exit the loop when the `q` key is pressed.

### Key Components

- **Gaussian Blur:** Reduces noise and smooths the image for better color detection.
- **HSV Conversion:** Converts BGR colors to HSV, which is easier for color-based segmentation.
- **Morphological Transformations:** Removes noise from the mask using the `cv.morphologyEx()` function.
- **Contour Detection:** Finds the largest contour, then calculates and draws a bounding rectangle around the detected object.

Once the script is running, the webcam feed will open. The yellow and pink objects in the video will be detected and highlighted with blue bounding boxes. Press `q` to close the webcam feed and exit the program.

## Customization

- **Add More Colors:** You can track additional colors by adding them to the script in the BGR format and using the `getLimits()` function to calculate the HSV range.
- **Adjust Color Tolerance:** Modify the tolerance in `getLimits()` to fine-tune color detection. Increase or decrease the HSV range around the target color.
- **Modify Blur & Morph Settings:** The script uses Gaussian blur and morphological opening to reduce noise. You can adjust the kernel size or blur parameters to achieve better results.