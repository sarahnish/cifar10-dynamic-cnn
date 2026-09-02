# CIFAR-10 Classification with a Dynamically Weighted Multi-Branch CNN

<p align="center">
  <b>A PyTorch image-classification project exploring input-dependent convolutional branch weighting on CIFAR-10.</b>
</p>

## Quick Links

<p align="center">
  <a href="notebooks/cifar10-dynamic-cnn.ipynb">Modelling Notebook</a> •
  <a href="results/README.md">Evaluation Results</a> •
  <a href="https://github.com/sarahnish/portfolio">Project Portfolio</a>
</p>

## At a Glance

| Dataset | Training Images | Test Images | Baseline | Improved |
|---|---:|---:|---:|---:|
| **CIFAR-10** | **50,000** | **10,000** | **83.57%** | **91.08%** |

> **+7.51 percentage-point improvement in best test accuracy**

## The Idea

Standard convolutional layers apply a fixed transformation to every input.

This project explores a different mechanism: within each intermediate block, several convolutional branches process the same feature map in parallel. Their outputs are combined using input-dependent weighting coefficients learned from the incoming feature representation.

For each image, an intermediate block:

1. computes the average value of each input channel
2. passes those values through a fully connected layer to generate branch coefficients
3. processes the same feature map through multiple convolutional branches
4. combines the branch outputs using the input-dependent coefficients

The result in the network shown that can vary how strongly it uses different convolutional branches depending on the input image.

Two configurations are evaluated:

- **Baseline model** — a smaller three-block dynamically weighted CNN
- **Improved model** — a deeper and wider configuration with additional branches, batch normalisation, dropout and an extended training strategy

The improved model achieved **91.08% test accuracy**, compared with **83.57%** for the baseline, an improvement of **7.51 percentage points**.


## Architecture

```text
Input Image
     │
     ▼
Dynamic Multi-Branch Block
     │
     ├── Conv Branch 1 ─┐
     ├── Conv Branch 2 ─┼──► Weighted Combination
     └── Conv Branch N ─┘
              ▲
              │
      Input-dependent
        coefficients
              │
     Channel Averaging
