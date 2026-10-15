# Pothole Detection Using YOLOv8

## Overview

Potholes are a common road hazard that can affect vehicle safety and ride comfort. This project uses computer vision to detect potholes in road videos and highlight the detected regions, making the output easier to inspect.

The system trains a YOLOv8 object detection model on a pothole dataset and applies the trained model to videos frame by frame. It also includes a simple active suspension visualization to demonstrate the concept of a suspension response.

## How It Works

1. **Dataset preparation:** Training and validation images and YOLO-format labels are copied from Google Drive into the notebook's working environment.
2. **Configuration:** A YAML configuration file defines the training and validation image paths and the single detection class, `pothole`.
3. **Model training:** A pretrained YOLOv8n model is fine-tuned on the dataset.
4. **Video inference:** The trained weights are loaded, and OpenCV reads an uploaded video frame by frame.
5. **Detection visualization:** YOLOv8 predictions are drawn on each frame, and the annotated frames are written to an output video.
6. **Output:** The notebook reports frame-processing information and downloads the generated video.

## Technologies Used

- **Python** — project implementation
- **Ultralytics YOLOv8n** — object detection and model training
- **OpenCV** — video input, frame processing, and output video generation
- **Matplotlib** — displaying detections and the suspension-response visualization
- **PyYAML** — generating the YOLO dataset configuration
- **Google Colab and Google Drive** — notebook execution and dataset access

## Training Configuration

The notebook uses the following training settings:

| Parameter | Configuration |
|---|---|
| Initial model | `yolov8n.pt` (pretrained YOLOv8 nano) |
| Training epochs | 10 |
| Image size | 320 |
| Batch size | 16 |
| Number of classes | 1 |
| Class name | `pothole` |
| Run name | `yolov8-pothole` |

The trained model weights are located from the Ultralytics run directories and loaded for video inference.

## Dataset Structure

The notebook expects the dataset in Google Drive at `MyDrive/PotholeDataset`:

```text
PotholeDataset/
├── train/
│   ├── images/
│   └── labels/
└── valid/
    ├── images/
    └── labels/
```

The image files and their corresponding `.txt` annotation files should follow the YOLO dataset format. The notebook configures the dataset with one class: `pothole`.

## Video Processing

When the notebook runs the inference workflow, it prompts the user to upload a video. OpenCV reads the video's properties, including resolution, frame rate, and frame count. Each frame is passed to the trained YOLOv8 model, and the model's plotting function draws the detections.

The processed frames are written to:

```text
pothole_detected_output.mp4
```

The notebook also reports the total number of frames processed and the number of frames containing at least one detection. Its reported detection rate is the percentage of processed frames with detections; it is **not** a model accuracy or precision score.

## Suspension-Response Visualization

The notebook contains a Matplotlib animation function that displays a basic suspension-response concept. It is a visual demonstration only: it does not use vehicle sensor data, implement a validated vehicle-dynamics model, or control real suspension hardware.

## Running the Project

1. Open `CV_Mini_Project.ipynb` in Google Colab.
2. Mount Google Drive when prompted.
3. Place the dataset in the expected `PotholeDataset` folder structure.
4. Run the notebook cells in order to prepare the data and train the model.
5. Run the video-processing cell and upload a road video.
6. View or download `pothole_detected_output.mp4`.

## Scope and Limitations

This project demonstrates pothole object detection and annotated video generation. Detection performance depends on the dataset, image conditions, and video quality. The notebook's current configuration uses 10 training epochs and an image size of 320. It does not report a formal evaluation using metrics such as precision, recall, or mAP, so no specific accuracy is claimed.

The project is intended for educational and experimental use, not as a safety-critical road-monitoring or vehicle-control system.
