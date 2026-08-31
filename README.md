# MLAdversary

## Project Overview
**MLAdversary** explores the security vulnerabilities inherent in modern computer vision systems. Machine learning models, while highly accurate on clean data, are often highly susceptible to carefully crafted, human-imperceptible perturbations known as **adversarial examples**. 

This project tackles both offensive and defensive machine learning security:
1. **Red Teaming (Attack):** We deploy multiple adversarial attack algorithms to drastically degrade the performance of a baseline image classifier (`<YOUR MODEL, e.g., ResNet-18>`) trained on `<YOUR DATASET, e.g., CIFAR-10>`.
2. **Blue Teaming (Defense):** We implement defensive mitigation strategies to harden the model, reducing the Attack Success Rate (ASR) while attempting to preserve accuracy on benign, unperturbed data.

---

## Implemented Techniques

### The Attacks
*   **Fast Gradient Sign Method (FGSM):** A rapid, single-step white-box attack that uses the gradients of the neural network to create a perturbation image.
*   **Projected Gradient Descent (PGD):** An iterative, stronger extension of FGSM. Often considered the "universal first-order adversary" for evaluating true model robustness.
*   **<Optional 3rd Attack - e.g., Carlini & Wagner (C&W) or DeepFool>:** <Brief description of the algorithm's objective, like minimizing L2 distance while guaranteeing misclassification>.

### The Defenses
*   **Adversarial Training:** The most reliable empirical defense. We retrain the model from scratch, continuously generating PGD-based adversarial examples in the training loop and treating them as valid training data.
*   **<Optional 2nd Defense - e.g., Feature Squeezing / Input Smoothing>:** <Briefly explain how you reduce the search space available to the attacker by smoothing/quantizing the image before inference>.

---

## Repository Structure

```text
MLAdversary/
│
├── data/                  # Dataset cache (ignored in git)
├── models/                # Saved weights for Baseline and Hardened models
├── src/
│   ├── train.py           # Script to train the baseline classifier
│   ├── attacks.py         # FGSM, PGD, and other attack implementations
│   ├── defenses.py        # Adversarial training loops and input transformations
│   ├── evaluate.py        # Benchmarking script for Clean Acc vs. Robust Acc
│   └── model.py           # Neural network architecture definitions
│
├── notebooks/             # Jupyter notebooks for visualizing perturbations
├── requirements.txt       # Python dependencies (PyTorch, Torchattacks, etc.)
└── README.md
