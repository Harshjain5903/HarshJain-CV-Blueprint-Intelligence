# BluePrint-To-Vector-AI | Harsh Jain

### Advanced Computer Vision for Automated Construction Takeoffs
**Author:** Harsh Jain (Master’s Student in Computer Science @ UIC)
**Project Focus:** Semantic Segmentation, Object Detection, and Raster-to-Vector Conversion

---

## Project Overview
In the construction industry, "takeoffs"—the manual process of measuring and counting materials from blueprints—is a massive bottleneck. This project implements a **State-of-the-Art (SOTA)** research pipeline designed to automate this process. By utilizing deep learning architectures, the system identifies structural elements and converts flat raster images into high-fidelity mathematical vector data, aiming to accelerate cost estimation by up to 10x.

---

## Key Research & Technical Features
* **Instance & Semantic Segmentation**: Leverages a multi-stage pipeline to precisely identify individual structural elements like walls, windows, and doors.
* **Structural Intelligence**: Classifies elements into 8 specific architectural categories, distinguishing between Inner and Outer walls for accurate material estimation.
* **Topology Correction (GAN-based)**: Employs a Generative Adversarial Network (GAN) to correct missing or extra architectural symbols, ensuring high-integrity outputs.
* **Heuristic Simplification**: Implements geometric reasoning to smooth edges and convert pixel masks into concise, vectorized maps ready for CAD/BIM integration.

---

## Research Extensions & Active Development (by Harsh Jain)
1.  **Swin Transformer Integration**: Investigating the use of **Swin Transformer backbones** within a Cascade R-CNN framework to improve long-range spatial awareness in complex blueprints.
2.  **Optimized PDF Pipeline**: Developing a robust preprocessing module to handle high-resolution PDF vector reading with minimal data loss during rasterization.
3.  **OCR & Legend Mapping**: Exploring the integration of LayoutLM-based OCR to automatically map blueprint legends to identified structural icons.

---

## Technical Stack
* **Programming**: Python 3.7+ (Optimized for modular research execution)
* **Deep Learning Frameworks**: PyTorch 1.8.1, TorchVision
* **Computer Vision Libraries**: OpenCV, Scikit-image, Shapely
* **Data Processing**: NumPy, Pandas, Matplotlib

---

## Class Mapping & Domain Logic
The model recognizes and categorizes the following structural classes:
`0: Background` | `1: Outer wall` | `2: Inner wall` | `3: Window` | `4: Door` | `5: Open portal` | `6: Room` | `7: Frame`

---

## Environment Preparation
This project is configured for Python environment management using Conda:

```bash
# Create and activate the research environment
conda create -n blueprint-harsh python=3.7
conda activate blueprint-harsh

# Install core dependencies
conda install -y pytorch==1.8.1 torchvision==0.9.1 torchaudio==0.8.1 cudatoolkit=10.2 -c pytorch
conda install -y matplotlib Pillow scikit-image scikit-learn tensorboard shapely
pip install ruamel.yaml tqdm opencv_python

```

---

## Running the Pipeline

### 1. Instance Segmentation

Outputs the instance segmentation for each floorplan:

```bash
cd 01_instance_seg/
python predict_new.py --test_folder ../data/preprocess/fp_img

```

### 2. Semantic Classification

Classifies predicted instances into the 8 architectural classes:

```bash
cd 02_type_class/
python data_gen.py --test_folder ../data/preprocess/fp_img
python evaluate.py --config_path example.yaml --test_folder ../data/preprocess/fp_img

```

### 3. Vectorization & Simplification

Smoothes segmentation masks into concise maps for vectorization:

```bash
cd 05_simplification/
python actions.py --method rh

```
