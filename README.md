# Vehicle-detection
Built a vehicle detection project using a pretrained YOLO model. It detects cars, trucks and motorcycles in still images, such as a busy highway photo, and in a live webcam feed shown inside Jupyter, labeling each object with a bounding box and confidence score. 
# Vehicle Detection with YOLO

Detect cars, trucks and motorcycles in images and in a live webcam feed, with bounding boxes and confidence scores. Built with a pretrained YOLO model, OpenCV and Jupyter.

## Features

- Detects vehicles in still images (for example a busy highway photo)
- Live webcam detection shown inside the Jupyter notebook
- Class label and confidence score on every box
- No training needed: vehicles are part of the COCO classes that standard YOLO models already know

## Demo

Add your screenshots to a `results/` folder and link them here:

```
![Highway detection](results/highway_detection.png)
![Live webcam detection](results/webcam_detection.png)
```

## How it works

1. **Load** a pretrained YOLO model with Ultralytics.
2. **Image mode:** run the model on a photo, draw boxes with labels and confidence scores, and display the result.
3. **Webcam mode:** open the camera with OpenCV, run detection on each frame, and show the annotated frame in the notebook output, refreshing it in a loop.
4. **Stop** the live cell by interrupting the kernel (the camera is released in a `finally` block).

## Project structure

```
vehicle-detection/
├── vehicle_detection.ipynb    # rename to match your notebook file
├── sample_images/             # test images (use your own or free-to-use photos)
├── results/                   # output screenshots
├── requirements.txt
└── README.md
```

## Quick start

```bash
git clone <your-repo-url>
cd <your-repo>/vehicle-detection
python -m venv .venv
# Windows: .venv\Scripts\activate     macOS/Linux: source .venv/bin/activate
pip install -r requirements.txt
jupyter notebook
```

Open the notebook and run the cells in order. The model weights download automatically on the first run, so it needs internet.

### Webcam notes

- The webcam cell runs in a loop. **Interrupt the kernel** (the stop button) to end it; the camera is released afterwards.
- If the camera does not open, close other apps that use it (Zoom, Teams, browser tabs) or change the camera index in `cv2.VideoCapture(0)` to `1`.
- The webcam only works when Jupyter runs on your own computer. It does not work on Google Colab, which cannot access your local camera directly.

## Configuration

| Setting | Meaning |
|---|---|
| Model name | Which pretrained YOLO model to load. Smaller models are faster, larger ones more accurate. |
| Confidence threshold | Minimum score for a detection to be shown. Raise it to remove false positives. |
| Camera index | `0` is the default webcam. |
| Frame delay | The short `time.sleep` in the loop controls how fast frames refresh. |

## Limitations

- A pretrained model can only detect classes it was trained on. Vehicles work well; unusual objects will not be found. (See the [Retail Shelf Auditor](../retail-shelf-auditor) project for a case that needed a different model.)
- Distant, small or heavily overlapping vehicles in dense traffic may be missed or merged.
- Detecting objects shown on a phone screen works for testing, but a screen is not the same as a real scene, so scores will differ.
- Speed depends on your hardware. Without a GPU, the live feed may run at only a few frames per second.

## Troubleshooting

| Problem | Fix |
|---|---|
| Kernel dies on Windows/Anaconda | Add `import os; os.environ["KMP_DUPLICATE_LIB_OK"] = "TRUE"` at the very top of the notebook, then restart |
| Camera not opening | Close other apps using the camera, or try camera index `1` |
| Webcam feed is slow | Use a smaller model, lower the frame size, or use a GPU |
| `ModuleNotFoundError` | Run `pip install -r requirements.txt` in the same environment as Jupyter |

## Roadmap

- [ ] Count vehicles per class
- [ ] Track vehicles across frames
- [ ] Process video files and save the output
- [ ] Speed or lane-based analysis

## Built with

[Ultralytics YOLO](https://docs.ultralytics.com/), PyTorch, OpenCV, Jupyter.

## Credits

Add the source of any sample images you did not take yourself.

## License

Add a license of your choice (for example MIT). Ultralytics is licensed under AGPL-3.0, which may affect how you distribute derived work.
