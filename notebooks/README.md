# Notebooks

[← Back to Project Overview](../README.md)

## Main Notebook

[`cifar10-dynamic-cnn.ipynb`](cifar10-dynamic-cnn.ipynb)

This notebook contains the complete CIFAR-10 modelling and evaluation workflow for the dynamically weighted multi-branch CNN.

## Contents

- CIFAR-10 data loading and augmentation
- Dynamic multi-branch CNN architecture
- Baseline model implementation and training
- Improved model implementation and training
- Training and test performance comparison
- Learning-curve analysis
- Per-class accuracy analysis
- Final evaluation and discussion

## Headline Results

| Model | Best Test Accuracy |
|---|---:|
| Baseline CNN | **83.57%** |
| Improved CNN | **91.08%** |

The improved configuration increased test accuracy by **7.51 percentage points** while retaining the dynamically weighted multi-branch design.

The best improved-model checkpoint was reached at **epoch 57**, with **97.83% training accuracy** and **91.08% test accuracy**.

## Related Resources

- [Project Overview](../README.md)
- [Evaluation Results](../results/README.md)
