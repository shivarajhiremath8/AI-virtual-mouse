# AI Virtual Mouse

This project implements an AI-powered virtual mouse using hand gesture recognition. It allows users to control the computer mouse cursor and perform clicks using hand movements captured via a webcam. The system uses computer vision and machine learning to track hand landmarks and translate them into mouse actions.

## Features

- **Hand Tracking**: Real-time hand detection and landmark tracking using MediaPipe.
- **Cursor Control**: Move the mouse cursor by pointing with your index finger.
- **Gesture Recognition**: Perform left-click, right-click, double-click, and screenshot actions using specific hand gestures.
- **Smoothing**: Averaged cursor positions for smooth movement.
- **Debouncing**: Prevents rapid successive clicks.
- **Full Screen Coverage**: Cursor can move across the entire screen without boundaries issues.

## Technologies Used

- **Python**: Programming language for the application.
- **OpenCV**: For video capture and image processing.
- **MediaPipe**: For hand detection and landmark estimation.
- **PyAutoGUI**: For controlling the mouse and keyboard.
- **Pynput**: For handling mouse button presses.
- **Threading**: To separate video processing from mouse control for better performance.
- **NumPy**: For numerical operations (used indirectly through other libraries).

## How It Works

### Step-by-Step Explanation

1. **Video Capture**:
   - The application captures video frames from the default webcam using OpenCV's `VideoCapture`.

2. **Hand Detection**:
   - Each frame is processed by MediaPipe's Hands model, which detects hand landmarks (21 points per hand).
   - The model is configured with:
     - `min_detection_confidence=0.5`: Lower threshold for initial hand detection to capture hands at edges.
     - `min_tracking_confidence=0.5`: Lower threshold for tracking to maintain detection when hands are partially out of frame.
     - `max_num_hands=1`: Limits to one hand for simplicity.

3. **Gesture Recognition**:
   - Landmarks are extracted and used to calculate distances and angles between fingers.
   - **Mouse Movement**: Triggered when the thumb and index finger are close (distance < 50) and the index finger is extended (angle > 90°).
     - The index finger tip's position is mapped to screen coordinates.
     - Positions are smoothed by averaging over the last 3 frames to reduce jitter.
     - Cursor is moved using PyAutoGUI's `moveTo` function.
   - **Left Click**: Thumb and index finger close, middle finger bent, ring finger extended.
   - **Right Click**: Thumb and middle finger close, index finger extended, ring finger bent.
   - **Double Click**: Thumb, index, and middle fingers close.
   - **Screenshot**: All fingers close, thumb and index far apart.

4. **Mouse Control**:
   - Mouse movements are handled in the main thread for responsiveness.
   - Clicks are debounced with a 0.2-second delay to prevent accidental multiple clicks.
   - PyAutoGUI settings: `FAILSAFE = False` to disable failsafe, `PAUSE = 0` for no delay between actions.

5. **Display and Loop**:
   - Processed frames with hand landmarks drawn are displayed in a window.
   - The loop continues until 'q' is pressed.

### Optimizations Applied

- **Threading**: Initially used for mouse movement, but removed to avoid overhead; video processing and mouse control run in the same thread.
- **Frame Skipping**: Removed to ensure smooth video display.
- **Smoothing**: Reduced from 5 to 3 positions for better responsiveness.
- **Confidence Thresholds**: Lowered to 0.5 for better edge detection.
- **Boundary Clamping**: Ensures cursor stays within screen limits.
- **Kalman Filter**: Added for advanced smoothing and prediction of cursor movement, reducing jitter and improving accuracy.

## Installation and Setup

### Prerequisites

- Python 3.7 or higher
- Webcam (built-in or external)

### Installation Steps

1. **Clone the Repository**:
   ```
   git clone https://github.com/your-username/ai-virtual-mouse.git
   cd ai-virtual-mouse
   ```

2. **Install Dependencies**:
   ```
   pip install opencv-python mediapipe pyautogui pynput
   ```

3. **Run the Application**:
   ```
   python main.py
   ```

### Usage

- Run the script and position your hand in front of the webcam.
- Use the following gestures:
  - **Move Cursor**: Bring thumb and index finger close together, point with index finger.
  - **Left Click**: Close thumb and index, bend middle, extend ring.
  - **Right Click**: Close thumb and middle, extend index, bend ring.
  - **Double Click**: Close thumb, index, and middle fingers.
  - **Screenshot**: Close all fingers except thumb and index (keep them apart).
- Press 'q' in the video window to quit.

### Troubleshooting

- **Lag or Sticking**: Ensure good lighting and clear hand visibility. Adjust confidence thresholds if needed.
- **Cursor Not Reaching Edges**: Lower confidence values further or reposition camera.
- **Permission Issues**: Run as administrator if PyAutoGUI fails to control mouse.

## Project Structure

- `main.py`: Main application script.
- `util.py`: Utility functions for angle and distance calculations.
- `TODO.md`: List of optimizations applied.
- `README.md`: This file.

## Contributing

Feel free to fork the repository and submit pull requests for improvements.

## License

This project is open-source. Use at your own risk.
