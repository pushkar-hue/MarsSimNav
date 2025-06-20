
MarsSimNav: Autonomous Terrain-Aware Rover Path Planning
Overview

MarsSimNav is a deep learning and path planning system built to simulate autonomous Mars rover navigation using real NASA imagery. It leverages a DeepLabV3+ segmentation model trained on the AI4Mars dataset to classify Martian terrain types, followed by A* search for optimal path planning over hazardous terrain.
Features

    Semantic Segmentation with DeepLabV3+

    Custom PyTorch Dataset Pipeline for AI4Mars

    Terrain-Aware Path Planning using A* algorithm

    Terrain Cost Mapping: soil, bedrock, sand, and big rocks

    Visual Overlay of predicted rover path on Mars images

    Efficient data handling for large datasets (supports subsetting)

    Inference-ready model with reproducible outputs

Dataset

    Source: AI4Mars Dataset

    Images: Over 18,000 images from the Curiosity rover (MSL)

    Labels: Pixel-level annotations for soil, bedrock, sand, and big rocks

    Preprocessing: Optionally subset to 5,000 images for lightweight experimentation

Technologies Used

    Python 3.11

    PyTorch and Torchvision

    DeepLabV3+ with ResNet50 backbone

    NetworkX for path planning (A* algorithm)

    Matplotlib and PIL for visualization

    Google Colab for development and testing

Getting Started

Clone the repository:

git clone https://github.com/pushkar-hue/marssimnav.git
cd marssimnav

Install dependencies:

pip install -r requirements.txt

To run in Google Colab:

    Upload your trained model as deeplabv3_mars.pth

    Place sample Mars images in ai4mars-subset/images/

    Call plan_rover_path(image_path, model) to visualize paths

Path Planning Logic

    Predict segmentation mask for a Mars image using DeepLabV3+

    Convert mask into a terrain cost map

    Use A* search to compute the lowest-cost safe path

    Visualize the path overlay on both the mask and the original image

Terrain Classes and Costs
Terrain	Class ID	Cost
Soil	0	1
Bedrock	1	4
Sand	2	6
Big Rock	3	10

Pixels with unknown labels (e.g. masked/NULL) are assigned high cost or skipped.
Sample Results
Input Image	Segmentation Mask	Planned Path Overlay
mars_image.jpg	predicted_mask.png	planned_path_overlay.png
![WhatsApp Image 2025-06-19 at 22 18 53_f36541c7](https://github.com/user-attachments/assets/f114eeb2-7c70-4d8d-9735-c341a1f1f45a)
![WhatsApp Image 2025-06-19 at 22 18 53_0b331c52](https://github.com/user-attachments/assets/c9cc27d9-fb8a-42af-9c3c-609780ea976f)
![WhatsApp Image 2025-06-19 at 22 18 53_cec2d284](https://github.com/user-attachments/assets/a2530933-939d-421f-b085-8443c5dd9427)

Future Work

    Add support for D* Lite and real-time replanning

    Interactive terrain selection and goal input via UI

    Animated simulation of rover motion along the path

    Deployable web dashboard using Streamlit or Gradio

    Integration with planetary data system (PDS) metadata

Authors

    Pushkar Sharma (@pushkar-hue)
    Ved Thorat (@i3hz)

    AI4Mars Dataset by NASA JPL and collaborators
