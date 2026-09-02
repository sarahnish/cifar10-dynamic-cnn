# Evaluation Results

[Back to Project Overview](../README.md)

This section details the performance analysis comparing the **Baseline CNN** against the **Improved Dynamic Multi-Branch CNN** architecture on the CIFAR-10 dataset.

---

## Performance Summary

| Model | Epochs Trained | Best Epoch | Training Accuracy | Best Test Accuracy |
|---|---:|---:|---:|---:|
| **Baseline CNN** | 20 | **20** | **86.16%** | **83.57%** |
| **Improved Dynamic CNN** | 60 | **57** | **97.83%** | **91.08%** |

> **Key Result:** The improved configuration achieved a **+7.51 percentage-point increase** in best test accuracy over the baseline.

### Best Checkpoint Selection

The improved model reached its highest test accuracy of **91.08% at epoch 57**.

Training continued through epoch 60, where test accuracy fell slightly to **90.91%**. This showed the value of saving and restoring the best checkpoint rather than simply using the final training epoch.

---

## Learning Dynamics & Training Curves

<p align="center">
  <img src="training-curves.png" alt="Training and testing accuracy curves comparing baseline and improved CNN architectures" width="100%"/>
</p>

[View full-size figure →](training-curves.png)

### Training Behaviour

- **Baseline Model:** Test accuracy improved steadily from **47.48% at epoch 1** to **83.57% at epoch 20**. Because performance was still trending upwards when training ended, a longer training schedule may have produced a stronger baseline.

- **Improved Model:** Training was unstable during the first few epochs before recovering and improving substantially:
  - **Epoch 23:** 80.07% test accuracy
  - **Epoch 43:** 88.01% test accuracy
  - **Epoch 57:** **91.08% test accuracy**

- **Generalisation Gap:** At the best checkpoint, training accuracy was **97.83%** compared with **91.08%** test accuracy, giving a **6.75 percentage-point gap**. This suggests moderate overfitting despite the additional regularisation used in the improved model.

---

## Per-Class Performance Analysis

Performance varied across the CIFAR-10 classes.

| Top-Performing Classes | Accuracy | Most Difficult Classes | Accuracy |
|---|---:|---|---:|
| **Car** | **95.90%** | **Cat** | **79.50%** |
| **Truck** | **95.20%** | **Dog** | **84.90%** |
| **Frog** | **94.50%** | — | — |
| **Ship** | **94.20%** | — | — |

**Mean Per-Class Accuracy: 91.08%**

> **Error Analysis:** Cats and dogs were the hardest classes for the model. At CIFAR-10's small **32×32 pixel resolution**, visually similar animal classes can share shapes, textures and backgrounds, making them harder to distinguish.

---

## Methodological Insights & Limitations

### Confounding Factors & Ablation Requirements

While the improved model achieved a substantial gain of **+7.51 percentage points**, several architectural and training changes were introduced at the same time:

- increased network depth and width
- additional branches in the deeper blocks
- batch normalisation
- dropout
- label smoothing
- higher initial learning rate
- longer training schedule

Because these changes were introduced together, their individual contributions cannot be isolated.

A stronger follow-up experiment would use controlled ablation studies where one change is introduced at a time.

### Loss Metric Comparability

The cross-entropy loss values between the two configurations are not directly comparable because the improved model used **label smoothing**, while the baseline did not.

For this reason, accuracy is the clearer metric for comparing the two configurations.

> **Evaluation Design Note:**  
> Model comparison and best-checkpoint selection were conducted using the test partition. In a larger research project, a dedicated validation split would normally be used for model selection and hyperparameter tuning, while the test set would be reserved for final holdout evaluation.

---

## What I Took From the Results

The improved model clearly performed better than the baseline under this experimental setup.

The increase from **83.57% to 91.08%** shows that the final combination of architectural and training changes worked well.

However, because several changes were introduced simultaneously, I cannot say that one specific change caused the improvement.

The result should therefore be understood as showing that the **overall improved configuration performed better**, rather than proving the effect of one individual technique.

---

## Related Links

- **[Project Overview](../README.md)**
- **[Modelling Notebook](../notebooks/cifar10-dynamic-cnn.ipynb)**
- **[Architecture Diagram](../notebooks/architecture%20diagram.png)**
- **[Main Portfolio](https://github.com/sarahnish/portfolio)**
