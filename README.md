
# MarsSimNav: Autonomous Terrain-Aware Rover Path Planning

[![Python](https://img.shields.io/badge/Python-3.11-blue.svg)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-DeepLabV3+-ee4c2c.svg)](https://pytorch.org/)
[![NASA](https://img.shields.io/badge/Dataset-AI4Mars-red.svg)](https://deep-learning-on-mars.github.io/dataset/)

MarsSimNav is a deep learning and path planning system designed to simulate autonomous Mars rover navigation using real NASA imagery. It leverages a **DeepLabV3+** segmentation model trained on the **AI4Mars dataset** to classify Martian terrain types, followed by **A* search** to calculate optimal paths over hazardous terrain.

---

## Features

* **Semantic Segmentation:** Powered by DeepLabV3+ with a ResNet50 backbone.
* **Custom Pipeline:** Specialized PyTorch Dataset handling for AI4Mars pixel-level annotations.
* **Terrain-Aware Path Planning:** Implements the A* algorithm via NetworkX.
* **Cost-Based Navigation:** Assigns navigation weights to different terrain types (soil, bedrock, sand, big rocks).
* **Visualization:** Generates visual overlays of the predicted rover path on original Mars surface images.
* **Scalable:** Supports subsetting for lightweight experimentation (e.g., 5,000 images).

---

##  Dataset

* **Source:** [AI4Mars Dataset](https://deep-learning-on-mars.github.io/dataset/) from NASA JPL.
* **Imagery:** Over 18,000 images captured by the Curiosity rover (MSL).
* **Labels:** Pixel-level annotations for:
    * **Soil:** Safe for traverse.
    * **Bedrock:** Stable but requires caution.
    * **Sand:** High risk of entrapment.
    * **Big Rocks:** Physical obstacles.

---

##  Technologies Used

* **Core:** Python 3.11, PyTorch, Torchvision
* **Algorithms:** DeepLabV3+, A* (NetworkX)
* **Data & Visualization:** Matplotlib, PIL, NumPy
* **Environment:** Google Colab / Linux

---

## Getting Started

### 1. Clone the repository
```bash
git clone [https://github.com/pushkar-hue/marssimnav.git](https://github.com/pushkar-hue/marssimnav.git)
cd marssimnav
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```
### 3. Usage (Colab/Local)

- Ensure your trained model is available as `deeplabv3_mars.pth`.

- Place sample Mars images in `ai4mars-subset/images/`.

- Run the inference script or call the planning function:

## Path Planning Logic

The system follows a 4-step pipeline to ensure safe navigation:

- **Inference:** Predict the segmentation mask using the DeepLabV3+ model.

- **Mapping:** Convert the mask into a Terrain Cost Map based on class IDs.

- **Search:** Use A* to find the lowest-cost path from start to goal coordinates.

- **Overlay:** Project the computed path onto the original image for visualization.

###  Terrain Cost
Terrain,Class ID,Cost Weight,Risk Level
Soil,0,1,Low
Bedrock,1,4,Moderate
Sand,2,6,High
Big Rock,3,10,Obstacle

Pixels with unknown labels (e.g. masked/NULL) are assigned high cost or skipped.

## Sample Results
Input Image	Segmentation Mask	Planned Path Overlay
mars_image.jpg	predicted_mask.png	planned_path_overlay.png
![WhatsApp Image 2025-06-19 at 22 18 53_f36541c7](https://github.com/user-attachments/assets/f114eeb2-7c70-4d8d-9735-c341a1f1f45a)
![WhatsApp Image 2025-06-19 at 22 18 53_0b331c52](https://github.com/user-attachments/assets/c9cc27d9-fb8a-42af-9c3c-609780ea976f)
![WhatsApp Image 2025-06-19 at 22 18 53_cec2d284](https://github.com/user-attachments/assets/a2530933-939d-421f-b085-8443c5dd9427)

## Future Work

- Add support for D* Lite and real-time replanning

- Interactive terrain selection and goal input via UI

- Animated simulation of rover motion along the path

- Deployable web dashboard using Streamlit or Gradio

- Integration with planetary data system (PDS) metadata

Authors

- **Pushkar Sharma** (@pushkar-hue)
- **Ved Thorat** (@i3hz)

*Special thanks to NASA JPL for providing the AI4Mars Dataset.*
