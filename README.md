# Rhinoceros Detection

This is the official repository for the paper ``Automated Rhinoceros Detection in Satellite Imagery using Deep Learning'' *Scienticic Reports*. The repository contains scripts and configuration files for training and evaluating a YOLOv12 object detection model to detect rhinoceroses in satellite imagery, including a pipeline for generating synthetic training data using Blender. 

## Structure

- **scripts/** – main Python code
  - `sim.py`: Uses the [Blender Python API](https://pypi.org/project/bpy/) (`bpy`) to generate synthetic satellite images of rhinoceroses.
  - `patch.py`: split large satellite images into smaller patches and update labels
  - `coco2yolo.py`: convert COCO JSON annotations to YOLO `.txt` labels
  - `yolo_run.py`: train YOLOv12 with configs
  - `detect.py`: evaluate trained models (mAP, etc.)
  - `tune.py`: search for best hyperparameters
- **sets/** – dataset configs (`data.yaml`, etc.)
- **hyperparams/** – training configs (learning rate, batch size, etc.)



## Usage

```bash
# Generate synthetic data
python scripts/sim.py

# Tile images into patches
python scripts/patch.py --in images_raw --labels labels_raw --out data_patched

# Convert COCO annotations to YOLO
python scripts/coco2yolo.py --coco coco/annotations.json --out labels_yolo

# Train YOLO
python scripts/yolo_run.py --data sets/data.yaml --hyp hyperparams/best_hyp.yaml --epochs 100

# Evaluate
python scripts/detect.py --data sets/data.yaml --weights runs/train/exp/weights/best.pt

# Hyperparameter tuning
python scripts/tune.py --data sets/data.yaml
```
## Google Drive For Blender Sim and Backgrounds  
#Blender project files and backgrounds:https://drive.google.com/drive/folders/131eGJ5P7uJMqY3SAge9DGGt4Ew7bsrtA?usp=drive_link

## Citation

If you use this repository, please cite:

```bibtex
@article{duporge2025rhinodetection,
  title   = {Automated Rhinoceros Detection in Satellite Imagery using Deep Learning},
  author  = {Duporge, I. and Lin, X. and Palnitkar, A. and Suresh, A. and Isupova, O. and Rubenstein, D. and Aloimonos, J. Y.},
  journal = {Scientific Reports},
  year    = {2025}
}


