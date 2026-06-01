# CNN Architecture Study

Eight controlled image-classification experiments, each isolating a single variable: architecture depth, hyperparameters, regularization, optimization, and transfer learning. All experiments use one shared dataset and preprocessing pipeline for fair comparison.

`Python` `PyTorch` `CNN` `Transfer Learning` `Weights & Biases` `Optuna`

> **Best result: 94.7% validation accuracy with a fine-tuned ResNet18.** Feature extraction reached 94.5% using only 5,130 trainable parameters, the same backbone trained from scratch reached 77.7%.

---

## Results

| Model | Best val acc | Best val loss | Trainable params |
|---|---|---|---|
| ResNet18 fine-tuned | **0.9468** | 0.1988 | 11.2M |
| ResNet18 feature extract | 0.9447 | **0.1730** | **5,130** |
| ResNet18 from scratch | 0.7768 | 0.7631 | 11.2M |
| ModelD from scratch | 0.6322 | 1.0639 | 305K |

*All models trained for 12 epochs.*

## Approach

Eight controlled experiments, each varying one factor:

| # | Topic | What was varied |
|---|---|---|
| 1 | Depth comparison | Shallow vs. deep custom CNNs under identical setup |
| 2 | Hyperparameter tuning | Learning rate, batch size, weight decay |
| 3 | Generalization regimes | Underfitting, good fit, overfitting under controlled data budgets |
| 4 | Regularization | Dropout, weight decay, early stopping |
| 5 | Optimizer comparison | SGD, SGD with momentum vs. adaptive optimizers (Adam, RMSprop) |
| 6 | Advanced architectures | Custom CNN (ModelD) vs. DenseNet121 |
| 7 | Experiment tracking | Weights & Biases logging, Optuna hyperparameter search |
| 8 | Transfer learning | Pretrained vs. from-scratch ResNet18, feature extraction vs. fine-tuning |

## Key Findings

**Transfer learning dominates at limited training budgets.** Both pretrained ResNet18 variants exceeded 0.94 validation accuracy within 12 epochs. The best from-scratch model (ResNet18, 0.7768) remained far below, showing the performance gap comes primarily from pretrained representations, not architecture alone.

**Feature extraction is the most parameter-efficient strategy.** ResNet18 feature extraction reached 0.9447 validation accuracy with only 5,130 trainable parameters, and the train-validation gap was essentially zero. This indicates stable generalisation without overfitting.

**Fine-tuning achieves the highest peak but overfits later.** Fine-tuning reached the best single-epoch validation accuracy (0.9468 at epoch 7), but the final train-validation gap (0.047) and high training accuracy (0.9885) suggest the model began to overfit after the optimal checkpoint.

**Optimization and regularization matter as much as architecture.** The same model produced very different results depending on learning rate, weight decay, and optimizer. Adaptive optimizers consistently outperformed SGD variants, and mild weight decay gave the best generalisation balance.

## Visualisations

### Optimizer comparison

Adam and RMSprop converge clearly faster than SGD and SGD with momentum. Plain SGD fails to make meaningful progress within 25 epochs under this setup.

<img src="assets/optimizer_comparison_accuracy.png" alt="Optimizer comparison" width="800">

### Transfer learning comparison

<img src="assets/transfer_learning_accuracy.png" alt="Transfer learning accuracy comparison" width="800">
<img src="assets/transfer_learning_loss.png" alt="Transfer learning loss comparison" width="800">

## Reproducibility

**Run**

```bash
git clone https://github.com/JananthanU/cnn-architecture-study
cd cnn-architecture-study
pip install -r requirements.txt
# Place an image-classification dataset under data/ (see below)
jupyter notebook cnn_experiments_icosimalv3.ipynb
```

**Data**

The original dataset (iCoSimal V3) is course-internal and not publicly available. The pipeline is dataset-agnostic and transfers to a public benchmark such as CIFAR-10 (or any folder-structured image dataset) with minimal change.

## Limitations

- The original dataset is **course-internal**, so the exact numbers are not reproducible as-is. The experiments are fully documented in the notebook, and the pipeline runs on public datasets with minimal adaptation.
- Each configuration was trained for a fixed 12-epoch budget and reported as a single run, longer training or multiple seeds could shift the ranking.
- "Best val acc" is the best single-epoch checkpoint, which slightly favours configurations that peak early before overfitting.
