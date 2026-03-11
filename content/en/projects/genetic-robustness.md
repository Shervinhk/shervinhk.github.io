---
title: "Robust and Interpretable Deep Learning for Genomic Data"
date: 2023-08-01
featured_image: "/images/robust.png"
omit_header_text: true
description: "Built adversarially trained deep learning models for genomics to test sensitivity of gene expression predictions to small perturbations and improve biological interpretability for drug discovery."
summary: "Adversarially trained genomic models to improve robustness and interpretability of gene expression predictions."
math: true
---



I contributed to the ideation and implementation of adversarial robustness experiments for deep learning models applied to single cell RNA-seq classification. The broader study examined how robustness training affects predictive stability and interpretability in genomic models.

Related publication: Bioinformatics Advances (2023) — [https://academic.oup.com/bioinformaticsadvances/article/3/1/vbad166/7444320](https://academic.oup.com/bioinformaticsadvances/article/3/1/vbad166/7444320) (See Acknowledgments)

## Problem: Accurate models can still be fragile

Deep learning classifiers trained on single cell RNA-seq can achieve high predictive accuracy, but small perturbations in gene expression can significantly change predictions. RNA-seq is noisy, biology should not destabilize outputs, and feature importance should highlight meaningful genes. We wanted to see whether adversarial training improves robustness here and how it affects interpretability.

## Task and data

Supervised cell type classification from gene expression vectors.

Datasets:
- Simulated SERGIO single cell data
- Mouse hippocampus data
- Mouse pancreas data

Model:
- Multilayer perceptron with fully connected hidden layers
- Softmax output
- Cross entropy loss

For input \(x\) and label \(y\), objective: \(L(f(x), y)\) where \(f(x)\) is the network output.

## Adversarial training

Adversarial examples were generated with:

- **Fast Gradient Sign Method (FGSM):**

  $$
  x_{\text{adv}} = x + \epsilon \cdot \operatorname{sign}\bigl(\nabla_x L(f(x), y)\bigr)
  $$

- **Projected Gradient Descent (PGD):** iterative FGSM with projection into an $\epsilon$-ball,

  $$
  x_{k+1} = \Pi_{B_\epsilon(x)} \Bigl[\, x_k + \alpha \cdot \operatorname{sign}\bigl(\nabla_x L(f(x_k), y)\bigr) \Bigr]
  $$

Training mixed clean and adversarial samples to harden the model. FGSM and PGD attacks were used to test robustness. I designed the adversarial setup, implemented the pipeline, ran FGSM/PGD experiments, and evaluated sensitivity under perturbations.

## Interpretability methods

We evaluated saliency maps, activation maximization, DeepLIFT, DeepSHAP, LIME, and gradient based attribution. Checks included stability of gene rankings under perturbation, agreement across methods, overlap with differentially expressed genes, and functional enrichment.

## Results

- Standard models were sensitive to small input changes; FGSM and PGD dropped accuracy.
- Adversarial training improved stability under attack.
- Robust training increased agreement between interpretability methods, stabilized gene rankings, and improved overlap with biologically meaningful genes. Pathway enrichment became more consistent.

The takeaway: making models robust can also make their explanations more reliable.

## Contribution and reflection

Accuracy alone is insufficient in scientific machine learning. Stability under perturbation is critical in high dimensional biological systems. Contributing to the robustness component of this study strengthened my interest in building models that are not only predictive, but stable and interpretable. This is important for genomics and drug discovery where reliability matters.
