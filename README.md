# AI Virtual Mouse

Welcome to the AI Virtual Mouse project! This Python application lets you control your computer mouse using hand gestures captured by your webcam. No touching required – just wave your hand and control your cursor!

---

## What is This?

The AI Virtual Mouse uses Computer Vision and Machine Learning to detect your hand movements in real time. It translates gestures into mouse actions like moving the cursor, clicking, and taking screenshots. Perfect for presentations, accessibility, or experimenting with tech!

---

## Key Features

- Real-Time Tracking: Detects your hand instantly with MediaPipe.
- Smooth Cursor Control: Move the mouse by pointing your index finger.
- Gesture Magic:
  - Left Click
  - Right Click
  - Double Click
  - Screenshot Capture
- Smart Smoothing: Reduces jitter for smooth movement.
- Debouncing: Prevents accidental double-clicks.
- Full-Screen Fun: Works across your entire display.

---

## Tech Stack

| Tool | What It Does |
|------|--------------|
| Python | The brain of the operation |
| OpenCV | Handles video capture and processing |
| MediaPipe | Spots and tracks your hand landmarks |
| PyAutoGUI | Automates mouse and keyboard actions |
| Pynput | Manages precise mouse clicks |
| NumPy | Crunches numbers for coordinates |
| Threading | Keeps everything running smoothly |

---

## How Does It Work? (Step-by-Step)

1. Capture Video: Your webcam grabs live frames.
2. Detect Hands: MediaPipe finds 21 key points on your hand.
3. Analyze Gestures: Code checks finger angles and distances.
4. Translate to Actions: Gestures become mouse commands.
5. Smooth & Execute: Kalman filter predicts movement for accuracy.

Gesture Guide:
- Move Cursor: Extend index finger, keep thumb close.
- Left Click: Close thumb and index, bend middle finger.
- Right Click: Close thumb and middle, extend index.
- Double Click: Close thumb, index, and middle.
- Screenshot: Close all fingers except thumb and index.

---

## Performance Boosts

We've optimized for speed and smoothness:
- Kalman Filter: Predicts cursor path to reduce lag.
- Debouncing: Adds tiny delays to stop click spam.
- Boundary Checks: Keeps cursor on-screen.
- Tuned Settings: Lower thresholds for better detection.

---

## Get Started (Easy Setup!)

### Requirements
- Python 3.7+
- Webcam (built-in or external)
- Good lighting for best results

### Installation Steps

1. Download the Code
   ```
   git clone https://github.com/yourusername/AI-virtual-mouse.git
   cd AI-virtual-mouse
   ```

2. Install Libraries
   ```
   pip install opencv-python mediapipe pyautogui pynput numpy
   ```

3. Run It!
   ```
   python main.py
   ```

4. Use It: Wave your hand in front of the camera. Press q to quit.

---

## Tips & Tricks

- Lighting Matters: Bright, even light helps detection.
- Steady Hands: Slow, smooth movements work best.
- Permissions: Allow camera access if prompted.
- Troubleshoot:
  - Lag? Close other apps or improve lighting.
  - No detection? Check camera and restart.

---

## Project Files

```
AI-Virtual-Mouse/
├── main.py          # Main app (start here!)
├── util.py          # Helper math functions
└── README.md        # This guide
```

---

## Future Ideas

- Multi-hand support for advanced gestures.
- Voice commands combo.
- Custom gesture trainer.
- Mobile app version.

---

## Contribute

Love this project? Help improve it!
1. Fork the repo.
2. Make your changes.
3. Submit a pull request.

Follow Python best practices and add comments to your code.

---

Enjoy controlling your mouse with gestures! If you have questions, open an issue. Happy coding!
