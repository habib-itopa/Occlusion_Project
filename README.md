
# Neuromatch Academy Deep Learning Project
# Investigating the Effect of Occlusion and Standard Data Augmentation on CNN and ResNet18 for Binary Image Classification
### Phase 1 – Local CIFAR-100 Fox/Wolf Preparation
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/habib-itopa/Occlusion_Project/blob/main/Phase_1_Local_CIFAR100_Fox_Wolf_Preparation.ipynb)

## Overview

Occlusion is a common challenge in computer vision where important parts of an object are hidden by other objects or missing from the image. Models that perform well on clean images may experience significant performance degradation when discriminative visual features are partially obscured.

This project investigates the robustness of two convolutional neural network architectures—a custom Simple CNN and ResNet18—on a binary image classification task consisting of **Fox** and **Wolf** images from the CIFAR-100 dataset. The study evaluates both architectures under increasing levels of artificial occlusion and further examines whether standard data augmentation improves robustness.

---

## Research Questions

This project addresses the following questions:

1. Which architecture is more robust to image occlusion?
2. Does standard data augmentation improve clean-image classification?
3. Does standard data augmentation improve robustness to occlusion?
4. Which image regions are most important for classification?
5. Does higher clean-image accuracy necessarily imply greater robustness?

---

## Dataset

The experiments use a binary subset of the **CIFAR-100** dataset.

Classes:

- Fox
- Wolf

Dataset statistics:

| Split | Images |
|--------|--------|
| Training | 800 |
| Validation | 200 |
| Test | 200 |

The same train/validation split is reused across all experiments to ensure fair comparisons.

---

## Models

### Simple CNN

A custom convolutional neural network consisting of:

- 3 Convolutional layers
- ReLU activations
- Max Pooling
- Dropout
- Fully connected classifier

---

### ResNet18

A modified ResNet18 adapted for CIFAR-100 by:

- replacing the initial 7×7 convolution with a 3×3 convolution,
- removing the initial max-pooling layer,
- replacing the final classification layer with a two-class output layer.

---

## Experiments

### Experiment 1 — Baseline Models

Models were trained without data augmentation.

Evaluations included:

- Clean test accuracy
- Increasing center occlusion
- Occlusion location analysis
- Confusion matrices
- Precision, Recall and F1-score

---

### Experiment 2 — Standard Data Augmentation

The models were retrained using standard online data augmentation.

Training augmentation:

- Random Crop
- Random Horizontal Flip
- Random Rotation
- Color Jitter

Validation and test images were **not augmented**.

The same evaluation protocol from Experiment 1 was repeated.

---

## Occlusion Experiments

Artificial square occlusions were introduced into test images.

### Occlusion Sizes

- 0×0
- 4×4
- 8×8
- 12×12
- 16×16
- 20×20
- 24×24

---

### Occlusion Locations

- Top Left
- Top Right
- Center
- Bottom Left
- Bottom Right
- Random

---

## Results Summary

### Clean Accuracy

| Model | Accuracy |
|--------|---------:|
| CNN | 90.5% |
| CNN + Augmentation | **93.0%** |
| ResNet18 | **89.5%** |
| ResNet18 + Augmentation | 89.0% |

Standard augmentation significantly improved the Simple CNN but had little effect on ResNet18.

---

### Robustness to Occlusion

As occlusion size increased, the performance of both models decreased.

However,

- the CNN achieved higher accuracy under mild occlusion,
- while ResNet18 maintained better performance under severe occlusion.

For example:

| Model | Clean | 16×16 | 20×20 | 24×24 |
|--------|------:|------:|------:|------:|
| CNN + Aug | 93.0% | 74.0% | 59.0% | 52.5% |
| ResNet18 + Aug | 89.0% | **75.5%** | **69.0%** | **60.5%** |

---

### Effect of Occlusion Location

Center occlusion consistently produced the largest reduction in accuracy.

Corner occlusions resulted in only minor performance degradation.

This indicates that both models rely primarily on central object features for classification.

---

### Confusion Matrix Analysis

Under severe occlusion:

- both models became more likely to misclassify foxes,
- wolf images remained easier to classify,
- ResNet18 maintained better class balance than the Simple CNN.

---

## Key Findings

- Standard augmentation improved the generalization ability of the Simple CNN.
- ResNet18 showed only marginal improvement from standard augmentation.
- ResNet18 remained the most robust model under severe occlusion.
- Higher clean-image accuracy did not necessarily correspond to greater robustness.
- Center image regions contain the most discriminative visual information.

---

## Repository Structure

```text
project/
│
├── data/
│
├── checkpoints/
│
├── experiment_1_baseline.ipynb
│
├── experiment_2_standard_augmentation.ipynb
│
├── results/
│
├── README.md
│
└── requirements.txt
```

---

## Requirements

- Python 3.10+
- PyTorch
- torchvision
- NumPy
- pandas
- matplotlib
- scikit-learn
- tqdm

Install dependencies using:

```bash
pip install -r requirements.txt
```

---

## Reproducibility

To reproduce the experiments:

1. Download the CIFAR-100 dataset.
2. Generate the binary Fox/Wolf subset.
3. Train the baseline models.
4. Train the augmented models.
5. Run the occlusion evaluation notebooks.
6. Compare the generated results with those reported in this repository.

Random seeds are fixed throughout the experiments to ensure reproducibility.

---

## Future Work

Potential extensions include:

- Random Erasing (occlusion-aware augmentation)
- CutMix
- MixUp
- Vision Transformers
- Grad-CAM visualization
- Occlusion sensitivity heatmaps
- Additional CIFAR-100 class pairs

---

## Authors


Topic:

**Investigating the Effect of Occlusion and Standard Data Augmentation on CNN and ResNet18 for Binary Image Classification**
