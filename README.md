# Air Canvas - Write and Erase with Hand Gestures

Air Canvas turns a Windows laptop webcam into a drawing surface. Raise your index finger and trace a word in the air to see it appear over the live video. Open your palm and sweep over a stroke to erase it. Press **S** to save the drawing as a PNG.

## Run locally

You need Python, a webcam, and camera access on Windows. The app uses OpenCV's DirectShow camera backend.

```powershell
git clone https://github.com/mhmdolleik-fullstack/writing-and-erasing-python.git
cd writing-and-erasing-python
python -m pip install opencv-python mediapipe numpy
python air_writing.py
```

The app looks for `hand_landmarker.task` beside the script. If the file is missing, it downloads the MediaPipe model on first launch. Allow internet access for that download.

## Controls

| Input | Action |
| --- | --- |
| Raise only your index finger in Draw mode | Draw with your fingertip |
| Open your palm | Erase beneath your palm |
| Close your hand after erasing | Return to Draw mode, then point to start a new stroke |
| Click a toolbar color | Select the ink color and return to Draw mode |
| `+` / `-` | Increase or decrease line thickness |
| `]` / `[` | Increase or decrease eraser size |
| `C` | Clear the canvas |
| `S` | Save the canvas as a timestamped PNG beside the script |
| `Esc` | Quit |

## How it works

A background thread captures webcam frames. MediaPipe tracks hand landmarks, and the app smooths fingertip coordinates before connecting them into strokes on a NumPy canvas. OpenCV overlays that canvas on the live preview. The saved PNG contains the drawing on a black background.

