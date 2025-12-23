# Data Annotation & Preprocessing Guide | Harsh Jain

This guide outlines the workflow for preparing custom floorplan datasets for the **BluePrint-To-Vector-AI** research pipeline.

## 1. Data Preparation
* Prepare floorplan images as high-resolution JPEG files.
* Place them in the project root under: `data/raw_img/`

## 2. Annotation Workflow
We utilize the **VIA (VGG Image Annotator)** tool for high-precision labeling.
* **Tool Access**: [VIA Annotation Tool](https://www.robots.ox.ac.uk/~vgg/software/via/via.html)
* **Setup**: Click `Project -> Add local files` to import your blueprints.
* **Attributes**: Add two region attributes: **"label"** and **"attribute"**.

### Labeling Categories
For architectural takeoffs, ensure regions are tagged with one of the following:
`outer`, `inner`, `window`, `door`, `portal`, `room`, `frame`

### Instance ID Logic
* Use the "attribute" field for instance tracking: `id_[pos/neg]`
* `id`: Unique integer for the specific instance.
* `pos/neg`: Use `pos` for a standard mask and `neg` to define holes (e.g., a central pillar in a room).

## 3. Export & Preprocessing
1. **Export**: Click `Annotation -> Export Annotations (as json)`.
2. **Save**: Rename to `via_annotations.json` and place in the `data/` folder.
3. **Generate Masks**:
   ```bash
   cd 00_preprocess/
   python generate_masks.py