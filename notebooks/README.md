# Modelling Notebook

[← Back to Project Overview](../README.md)

This folder contains the main modelling notebook for the CIFAR-10 Dynamic Multi-Branch CNN project.

The notebook covers the full workflow from data preparation and architecture implementation through model training, comparison and final evaluation.

---

## Main Notebook

### [`CIFAR10_CNN.ipynb`](CIFAR10_CNN.ipynb)

The notebook contains the complete PyTorch implementation of the dynamically weighted multi-branch CNN.

It compares two configurations:

- **Baseline CNN** — a smaller three-block dynamically weighted model
- **Improved Dynamic CNN** — a deeper and wider four-block model with additional branches, batch normalisation, dropout and an extended training strategy

[Open the full modelling notebook →](CIFAR10_CNN.ipynb)

---

## What the Notebook Covers

### 1. Data Preparation

- CIFAR-10 dataset loading
- training and test DataLoaders
- image normalisation
- random crop augmentation
- horizontal-flip augmentation
- batch and input-shape verification

### 2. Dynamic Multi-Branch Architecture

The core architecture uses several convolutional branches inside each intermediate block.

Each branch processes the same input feature map, while a separate weighting path generates **input-dependent coefficients** used to combine the branch outputs.

The notebook implements:

- reusable PyTorch `nn.Module` blocks
- parallel convolutional branches
- global channel averaging
- learned branch coefficients
- weighted branch combination
- configurable output layers

[View the architecture diagram →](architecture%20diagram.png)

### 3. Baseline Model

The baseline provides the starting point for comparison and retains the defining dynamic branch-weighting mechanism.

It is trained for **20 epochs** and reaches a best test accuracy of **83.57%**

### 4. Improved Model

The improved configuration increases model capacity and introduces several additional training and regularisation choices, including:

- four dynamic blocks
- increased channel width
- additional branches in deeper blocks
- batch normalisation
- hidden fully connected output layer
- dropout
- label smoothing
- higher initial learning rate
- longer training schedule

The improved model is trained for **60 epochs**.

### 5. Model Comparison

The notebook compares the training behaviour and final performance of both configurations.

| Model | Epochs | Best Epoch | Best Test Accuracy |
|---|---:|---:|---:|
| **Baseline CNN** | 20 | 20 | **83.57%** |
| **Improved Dynamic CNN** | 60 | 57 | **91.08%** |

> **The improved configuration increased best test accuracy by 7.51 percentage points.**

At its best checkpoint, the improved model achieved:

- **97.83% training accuracy**
- **91.08% test accuracy**
- **6.75 percentage-point training–test gap**

The best checkpoint occurred at **epoch 57**, rather than the final epoch.

### 6. Learning-Curve Analysis

The notebook tracks training and test accuracy across both experiments.

The baseline improved steadily throughout its shorter training schedule.

The improved model experienced early optimisation instability before recovering and eventually reaching substantially higher test accuracy.

[View evaluation results →](../results/README.md)

### 7. Per-Class Evaluation

The final model is also evaluated separately across the ten CIFAR-10 classes.

The strongest results included:

- **Car:** 95.90%
- **Truck:** 95.20%
- **Frog:** 94.50%
- **Ship:** 94.20%

The most difficult classes were:

- **Cat:** 79.50%
- **Dog:** 84.90%

The mean per-class accuracy was **91.08%**.

### 8. Discussion & Limitations

The notebook also examines the limitations of the experiment.

Several architectural and training changes were introduced simultaneously, so the **7.51 percentage-point improvement cannot be attributed to one individual change**.

The comparison is also limited by:

- a single random seed
- different training budgets
- no controlled ablation study
- use of the test partition during model comparison and checkpoint selection

These limitations are discussed alongside possible improvements for future experiments.

---

## Key Outputs

| Output | Location |
|---|---|
| Full modelling workflow | [`CIFAR10_CNN.ipynb`](CIFAR10_CNN.ipynb) |
| Architecture diagram | [`architecture diagram.png`](architecture%20diagram.png) |
| Training curves | [`../results/training-curves.png`](../results/training-curves.png) |
| Evaluation summary | [`../results/README.md`](../results/README.md) |

---

## Related Resources

- [Project Overview](../README.md)
- [Evaluation Results](../results/README.md)
- [Architecture Diagram](architecture%20diagram.png)
- [Project Portfolio](https://github.com/sarahnish/portfolio)
