# YOLOv5 Object Detection with TTS and CSV Logging

This project is a customized implementation of the YOLOv5 object detection framework. It supports real-time object detection via webcam, video files, image directories, or screen captures. Additionally, it integrates:

- 📢 **Text-to-Speech (TTS)** using `pyttsx3` for vocalizing detected object classes.
- 📄 **CSV Logging** for recording predictions with confidence scores.
- 🖼️ Image/Video output with bounding boxes and optional label hiding.

---

## 📌 Features

- Real-time object detection using webcam, screen, or video/image input.
- Uses [Ultralytics YOLOv5](https://github.com/ultralytics/yolov5) backend.
- Text-to-Speech output for detected object names.
- Save detection results to:
  - `.txt` files (YOLO or Pascal VOC format)
  - `.csv` file
  - Cropped images of detected objects
  - Annotated image/video output
- Supports GPU (`CUDA`) or CPU inference.
- Multi-platform compatible (Windows, Linux, macOS).

---

## 🛠️ Setup

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/yolov5-tts-csv.git
cd yolov5-tts-csv
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Download Weights

Make sure you have a YOLOv5 model weight (`best.pt` or any `.pt` file from training):

```bash
# Example using pre-trained yolov5s
wget https://github.com/ultralytics/yolov5/releases/download/v6.0/yolov5s.pt
```

---

## 🚀 Usage

Run detection using:

```bash
python detect.py --weights best.pt --source 0 --view-img --save-csv
```

### Arguments

| Argument        | Description                                                              |
|-----------------|--------------------------------------------------------------------------|
| `--weights`     | Path to model weights file (`.pt`).                                      |
| `--source`      | Input source: `0` for webcam, path to image/video, URL, or screen.       |
| `--data`        | Path to `data.yaml`.                                                     |
| `--imgsz`       | Inference image size. Default is 736.                                    |
| `--conf-thres`  | Confidence threshold for detection.                                      |
| `--iou-thres`   | IOU threshold for Non-Max Suppression.                                   |
| `--view-img`    | Show detection results in a popup window.                                |
| `--save-txt`    | Save predictions to label files.                                         |
| `--save-format` | Save format: `0` = YOLO, `1` = Pascal VOC.                               |
| `--save-csv`    | Save results to a `predictions.csv` file.                                |
| `--save-crop`   | Save cropped images of detected objects.                                 |
| `--hide-labels` | Hide labels on the output images/videos.                                 |
| `--hide-conf`   | Hide confidence scores from bounding box labels.                         |
| `--device`      | Use CUDA (`0`, `0,1`, etc.) or CPU (`cpu`).                              |

---

## 🔊 Text-to-Speech Integration

The code uses `pyttsx3` to read out the detected object name using your system's default voice. Speech runs in a separate thread to avoid blocking real-time detection.

---

## 📂 Output Files

Depending on flags used, output can include:

- Annotated images/videos with bounding boxes.
- Text label files under `runs/detect/exp*/labels/`.
- `predictions.csv` with `Image Name`, `Prediction`, and `Confidence`.

---

## 🧠 Key Components

- `run(...)`: Core function that loads model, runs inference, and processes results.
- `speech(...)`: TTS function using `pyttsx3`.
- `write_to_csv(...)`: Appends prediction results to a CSV file.
- `Annotator`: YOLOv5 utility for drawing boxes on frames.
- `parse_opt()`: Parses command-line arguments.

---

## 📦 Example Commands

Run with webcam and TTS:

```bash
python detect.py --weights best.pt --source 0 --view-img --save-csv
```

Detect from a video:

```bash
python detect.py --weights best.pt --source path/to/video.mp4 --save-img
```

Detect and save YOLO-format labels:

```bash
python detect.py --weights best.pt --source data/images --save-txt --save-format 0
```

---

## 📣 Credits

- [Ultralytics YOLOv5](https://github.com/ultralytics/yolov5)
- `pyttsx3` for Text-to-Speech
