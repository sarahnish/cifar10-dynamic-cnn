# CIFAR-10 Classification with a Dynamically Weighted Multi-Branch CNN

A PyTorch image-classification project exploring a dynamically weighted multi-branch convolutional architecture on CIFAR-10.

## Overview

This project implements a convolutional neural network in which multiple convolutional branches process the same feature map in parallel. Their outputs are combined using input-dependent weighting coefficients learned from the incoming feature representation.

Two configurations are evaluated:

- **Baseline model** — a smaller three-block dynamically weighted CNN
- **Improved model** — a deeper and wider configuration with additional branches, batch normalisation, dropout and an extended training strategy

The improved model achieved **91.08% test accuracy**, compared with **83.57%** for the baseline, an improvement of **7.51 percentage points**.
