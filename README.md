# Academic CNN Experiments on iCoSimal V3

## Project goal

This repository documents an academic deep-learning project on **convolutional neural networks applied to the iCoSimal V3 dataset**.  
The goal is to systematically investigate how architecture design, hyperparameter choices, regularization, optimization, and transfer learning affect classification performance and generalization.

## Why this project matters

Deep-learning performance does not depend on a single modelling choice.  
It emerges from the interaction between model architecture, training configuration, optimization strategy, and regularization. This project focuses on making these effects visible through controlled experiments rather than treating model training as a black-box process.

The repository is intended as a compact academic study that demonstrates both practical implementation and analytical interpretation of CNN experiments.

## What this repository demonstrates

- structured experimentation with convolutional neural networks
- comparison of CNN architectures with increasing depth and capacity
- analysis of hyperparameter sensitivity
- demonstration of underfitting, good fit, and overfitting regimes
- evaluation of regularization methods
- comparison of optimization algorithms
- exploration of advanced architectures
- experiment tracking with Weights & Biases
- automated hyperparameter search with Optuna
- transfer learning with pretrained vision models
- clear documentation of results and lessons learned

## Dataset

The experiments were conducted on the **iCoSimal V3 dataset** used in the course setting.

The dataset is **not included in this repository**.  
To reproduce the experiments, use your own local copy of the dataset and place it in an appropriate local data directory.

## Experimental scope

The notebook covers a sequence of experiments designed to study different aspects of CNN training and evaluation:

1. **Architecture comparison**  
   Progressive increase in CNN depth and capacity to study the effect of architectural complexity.

2. **Hyperparameter tuning**  
   Analysis of how learning rate, batch size, and weight decay influence training behaviour and final performance.

3. **Generalization regimes**  
   Explicit demonstration of underfitting, good fit, and overfitting.

4. **Regularization**  
   Comparison of techniques such as dropout, weight decay, and early stopping.

5. **Optimizer comparison**  
   Evaluation of different optimization algorithms and their effect on convergence and validation performance.

6. **Advanced architectures**  
   Comparison between a custom CNN and stronger reference architectures.

7. **Experiment tracking and automated search**  
   Use of **Weights & Biases** for monitoring and **Optuna** for automated hyperparameter optimization.

8. **Transfer learning**  
   Comparison between models trained from scratch and pretrained models using feature extraction and fine-tuning.

## Repository structure

```text
academic-cnn-experiments-icosimalv3/
├── README.md
├── LICENSE
├── .gitignore
└── cnn_experiments_icosimalv3.ipynb
```
## Current status
Completed academic deep-learning project. The repository contains the final notebook with the implemented experiments, results, and conclusions.
