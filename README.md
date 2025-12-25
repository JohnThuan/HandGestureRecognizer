# HandGestureRecognizer

A real-time hand gesture recognition system that detects hand gestures using your webcam and displays corresponding emoji reactions. Built with MediaPipe and OpenCV.

## Features

- **Real-time Hand Tracking**: Detects up to 2 hands simultaneously
- **Gesture Recognition**: Recognizes multiple hand gestures 


## Technical Stack

- **Python 3.8+**
- **MediaPipe**: Google's ML solution for hand tracking and gesture recognition
- **OpenCV (cv2)**: Real-time video capture and image processing
- **NumPy**: Array operations and image manipulation



### Dependencies

```bash
pip install mediapipe opencv-python numpy
```

### Required Assets

The application requires the following files in an `assets/` directory:

1. **Model File**:
   - `gesture_recognizer.task` - MediaPipe gesture recognition model

2. **Emoji Images**:
   - `nerd.png` - Displayed for "Pointing Up" gesture
   - `thumbs up.png` - Displayed for "Thumbs Up" gesture
   - `thumbs down.png` - Displayed for "Thumbs Down" gesture
   - `fours.png` - Displayed for "Fours" gesture
   - `shy.jpg` - Displayed for "Shy" gesture (both hands)
   - `mog.png` - Default emoji when no gesture detected

## Project Structure

```
hand-gesture-recognizer/
├── main.py                          # Main application file
├── assets/
│   ├── gesture_recognizer.task      # MediaPipe model
│   ├── nerd.png
│   ├── thumbs up.png
│   ├── thumbs down.png
│   ├── fours.png
│   ├── shy.jpg
│   └── mog.png
└── README.md
```

## Installation & Setup

1. **Clone or download the project**

2. **Install dependencies**:
```bash
pip install mediapipe opencv-python numpy
```

3. **Download MediaPipe gesture recognition model**:
   - Download from [MediaPipe Models](https://developers.google.com/mediapipe/solutions/vision/gesture_recognizer)
   - Place `gesture_recognizer.task` in the `assets/` folder

4. **Add emoji images**:
   - Create an `assets/` folder
   - Add all required emoji images (PNG/JPG format)

5. **Run the application**:
```bash
python main.py
```

## Usage

1. **Start the application**: Run the Python script
2. **Position yourself**: Ensure your hands are visible in the camera feed
3. **Perform gestures**: Try different hand gestures to see emoji reactions
4. **Quit**: Press 'q' to exit the application

## Recognized Gestures

### Standard Gestures (MediaPipe)
- **Pointing Up** (☝️): Index finger pointing upward
- **Thumbs Up** (👍): Classic thumbs up gesture
- **Thumbs Down** (👎): Thumbs down gesture

### Custom Gestures
- **Fours** (🤘): Custom gesture with specific finger positioning
  - Detected when thumb is positioned between index and pinky fingers horizontally
- **Shy** (🙈): Both hands covering face
  - Requires 2 hands with specific positioning where index fingers and thumbs align vertically

## Configuration

### Window Settings
```python
WINDOW_WIDTH = 720
WINDOW_HEIGHT = 450
```

### Detection Confidence Thresholds
```python
num_hands=2                          # Maximum number of hands to detect
min_tracking_confidence=0.4          # Minimum tracking confidence
min_hand_detection_confidence=0.7    # Minimum detection confidence
min_hand_presence_confidence=0.6     # Minimum presence confidence
```

### Display Settings
```python
MARGIN = 5                           # Pixels margin for text
FONT_SIZE = 0.75                    # Text font size
FONT_THICKNESS = 2                  # Text thickness
```

## How It Works

1. **Video Capture**: Opens webcam and captures video frames at 30 FPS
2. **Color Conversion**: Converts BGR (OpenCV) to RGB (MediaPipe)
3. **Gesture Recognition**: Processes each frame through MediaPipe's gesture recognition model
4. **Landmark Detection**: Identifies 21 hand landmarks per hand
5. **Custom Gesture Logic**: Additional logic for "Fours" and "Shy" gestures
6. **Visualization**: Draws hand skeleton and displays corresponding emoji
7. **Real-time Display**: Shows both annotated camera feed and emoji output

## Hand Landmarks

MediaPipe detects 21 landmarks per hand:
- 0: Wrist
- 1-4: Thumb (CMC, MCP, IP, TIP)
- 5-8: Index finger (MCP, PIP, DIP, TIP)
- 9-12: Middle finger
- 13-16: Ring finger
- 17-20: Pinky finger

## PyInstaller Support

The code includes resource path handling for PyInstaller bundling:

```python
def resource_path(relative_path):
    return (os.path.join(sys._MEIPASS, relative_path)
            if hasattr(sys, '_MEIPASS')
            else os.path.join(os.path.abspath("."), relative_path))
```

To create a standalone executable:
```bash
pyinstaller --onefile --add-data "assets:assets" main.py
```

## Troubleshooting

### Webcam not opening
- Ensure no other application is using the webcam
- Try changing camera index: `cv2.VideoCapture(1)` or `cv2.VideoCapture(2)`

### Emoji images not found
- Verify all emoji files exist in the `assets/` folder
- Check file names match exactly (case-sensitive)
- Ensure image formats are correct (PNG/JPG)

### Poor gesture recognition
- Improve lighting conditions
- Ensure hands are fully visible in frame
- Adjust confidence thresholds in code
- Keep hands at appropriate distance from camera

### High CPU usage
- Reduce frame processing rate
- Decrease window resolution
- Optimize emoji image sizes

## Performance Optimization

- **Image Sizes**: All emoji images are resized to 720x450 for consistent display
- **Frame Rate**: Runs at webcam's native FPS (typically 30 FPS)
- **Async Processing**: Uses MediaPipe's async recognition for better performance

## Future Improvements

- [ ] Add more custom gestures
- [ ] Implement gesture-based controls (volume, playback)
- [ ] Add gesture history/statistics
- [ ] Support for more than 2 hands
- [ ] Mobile app version
- [ ] Custom emoji upload feature
- [ ] Record and replay gesture sequences
- [ ] Gesture-based gaming integration

## Credits

- **MediaPipe**: Google's ML framework for hand tracking
- **OpenCV**: Open source computer vision library

## License

MIT License


## System Requirements

- **OS**: Windows, macOS, or Linux
- **Python**: 3.8 or higher
- **Webcam**: Built-in or USB webcam
- **RAM**: 4GB minimum (8GB recommended)
- **Processor**: Multi-core processor recommended for real-time processing

