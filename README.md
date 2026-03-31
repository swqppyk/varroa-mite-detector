# varroa-mite-detector

Binary image classifier that detects Varroa destructor mite infections in honeybees using MobileNetV2 transfer learning.
** 84% accuracy, 0.895 AUC **

## Background

Varroa destructor is a parasitic mite that attaches to honeybees and is one of the leading causes of colony collapse worldwide. Early detection is critical for beekeepers to treat infected hives before the mite spreads and devastates the colony.

This project builds a computer science vision model that classifies bee images as either **varroa infected** or **not infected**, providing a potential tool for automated hive monitoring.

---


## Results
| Metric           | Score |
|------------------|-------|
| Test Accuracy    | 84%   |
| AUC              | 0.895 |
| Varroa Precision | 0.57  |
| Varroa Recall    | 0.77  |
| Varroa F1 Score  | 0.65  |

---

## Model Structure
- **Backbone:** MobileNetV2 pretrained on ImageNet
- **Approach:** Two phase transfer learning
    - Phase 1: Frozen backbone, trained classification head only
    - Phase 2: Fine-tuned top layers of MobileNetV2 with early stopping
- **Input size:** 150x150 RGB images
- **Output:** Binary classification (varroa / not_varroa)
- **Framework:** TensorFlow / Keras

## Dataset

This project uses the BeeAlarmed dataset, created by the BeeAlarmed project,
licensed under the GNU General Public License (GPL). The dataset was obtained 
directly from the creator and contains labeled images of honeybees across 
multiple categories including varroa infected, healthy, cooling, pollen 
carrying, and wasp images.

Original project: https://github.com/BeeAlarmed/BeeAlarmed

### Data Cleaning
- Removed wasp images (not relevant to bee health detection)
- Converted multi-label annotations to binary classification
- Treated unlabeled images as healthy bees
- Split into 70% train / 15% validation / 15% test with stratification
- Applied class weights to handle class imbalance (1,266 varroa vs 5,274 not_varroa)

## Project Structure
```
varroa-mite-detector/
  notebooks/
    01_data_cleaning.ipynb
    02_model_training.ipynb
  README.md
  requirements.txt
  LICENSE
```

---

## How to Run

1. Clone the repository
```bash
git clone https://github.com/[YourUsername]/varroa-mite-detector.git
```

2. Install dependencies
```bash
pip install -r requirements.txt
```

3. Download the BeeAlarmed dataset from https://github.com/BeeAlarmed/BeeAlarmed
and place it in your Google Drive under `varroa_project/data/`

4. Run `01_data_cleaning.ipynb` to clean and split the dataset

5. Run `02_model_training.ipynb` to train and evaluate the model

---

## Requirements

- TensorFlow
- scikit-learn
- matplotlib
- Pillow
- numpy

---

## Future Improvements

- Train on higher resolution images (300x300) for more visual detail
- Collect more varroa-labeled images to improve precision
- Experiment with other backbones such as EfficientNetB0
- Build a simple web demo for real-world usage
- Explore object detection to locate the mite's exact position on the bee

---

## Author
Swathi Kabilan - Computer Science Student

## License

This project is licensed under the GNU General Public License v3.0 in accordance with the BeeAlarmed dataset license.
