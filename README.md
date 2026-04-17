# Sign-Lang-DETR 🧏‍♂️

> Real-Time Sign Language Detection using Transformer-Based Object Detection (DETR)

A deep dive into training an End-to-End Object Detection (DETR) model from scratch for recognizing and estimating sign language. This repository contains the full end-to-end pipeline: from custom data collection and labeling, all the way to training the transformers and running real-time inference on a webcam feed.

## 🚀 Key Features
- **Custom Data Collection Pipeline**: OpenCV-based script to capture and organize your own dataset.
- **Label Studio Integration**: Quick setup for efficient bounding-box annotations.
- **DETR Transformer**: Training scripts utilizing the power of Vision Transformers for object detection.
- **Real-Time Inference**: Run the trained model locally against your webcam with real-time bounding box overlay.

---

## 🪛 Setup & Installation

I recommend using [UV](https://github.com/astral-sh/uv) to manage the Python environment and dependencies securely.

1. **Install UV:**
   ```bash
   pip install uv
   ```
2. **Clone the Repository:**
   ```bash
   git clone https://github.com/tomcr00ze/sign-lang-DETR.git
   cd sign-lang-DETR
   ```
3. **Install Dependencies:**
   ```bash
   uv sync
   ```

---

## 📸 1. Collecting Images
If you want to train on your own signs, you can collect images directly through your webcam.

1. Open `src/utils/collect_images.py` and update the `classes` list with your target signs or gestures.
2. Run the collection script:
   ```bash
   uv run src/utils/collect_images.py
   ```
   *(A window will open; follow the prompts in the terminal to capture frames for each class.)*

## 🏷️ 2. Annotating Data
You need bounding box labels for the freshly captured images.

1. Ensure the labeling dependency is installed:
   ```bash
   uv pip list | grep label-studio
   ```
2. Launch the server:
   ```bash
   uv run label-studio
   ```
3. Create a new Data Collection setup pointing to your `data` directory and configure the bounding box layout.
   *Tip: Use `CTRL + Enter` to quickly submit labels as you move through your images!*

## 🦾 3. Training the DETR Model
To spin up the training loop based on your annotated dataset:

1. Create a directory to store model checkpoints:
   ```bash
   mkdir checkpoints
   ```
2. Start the training pipeline:
   ```bash
   uv run src/train.py
   ```
   *(Training times vary significantly depending on hardware acceleration.)*

## 🔮 4. Real-time Inference & Evaluation

To test your shiny new model against some held-out data:
1. Update your desired checkpoint tracking ID inside `src/test.py`.
   ```bash
   uv run src/test.py
   ```

**To use the real-time webcam detector:**
1. Point the script to the latest trained `.pt` checkpoint file in `src/realtime.py`.
2. Run the webcam instance:
   ```bash
   uv run src/realtime.py
   ```
*Note: If the camera doesn't start, map your specific camera ID by changing the parameter in `cv2.VideoCapture(0)`.*

---

## 👨🏾‍💻 Author & Info
- **Author:** Adarsh Jha (@tomcr00ze)
- **Version:** 1.0.0
- **License:** MIT License

Let me know if you do anything cool with this pipeline! Contributions and issues are welcome. 
