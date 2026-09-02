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

<p align="center">
  <img src="notebooks/architecture%20diagram.png" alt="Improved dynamically weighted multi-branch CNN block" width="900"/>
</p>

Each intermediate block sends the same input feature map through multiple convolutional branches. Global average pooling summarises the input channels, and a linear fully connected layer generates one input-dependent coefficient for each branch. Each branch output is multiplied by its corresponding coefficient before the weighted outputs are summed.

The improved network stacks four of these blocks with increasing channel capacity:

**3 → 64 → 128 → 256 → 512 channels** with max pooling reducing spatial resolution from **32×32 → 16×16 → 8×8 → 4×4**.
