---
title: "EEG Driven Brain Computer Interfaces for Assistive Mobility"
date: 2021-02-01
featured_image: "/images/eeg.png"
omit_header_text: true
description: "Designed and implemented an end to end EEG based BCI for real time wheelchair control using CSP feature extraction and frequency domain classification to translate neural signals into reliable movement commands."
summary: "EEG based BCI with CSP and frequency domain classifiers for real time wheelchair control."
math: true
---

During my undergraduate studies at Sharif University of Technology I developed an end to end EEG based brain computer interface system for assistive wheelchair control. The objective was to translate motor imagery signals into real time directional commands while ensuring reliability and safety.

## Problem: converting noisy brain signals into stable real time control

EEG signals are low amplitude, high dimensional, and easily contaminated by muscle and eye movement artifacts. For assistive mobility, a BCI must extract discriminative neural patterns, operate with low latency, minimize false activations, stay stable across sessions, and enforce safety constraints. The challenge was decoding motor imagery from scalp EEG and mapping it to wheelchair commands accurately and safely.

## Signal acquisition and preprocessing

- Recorded from multiple scalp electrodes over motor cortex
- Bandpass and notch filtering to isolate sensorimotor rhythms and remove power line noise
- Artifact reduction for ocular and muscular contamination
- Segmentation into fixed windows aligned with motor imagery tasks

## Feature extraction with Common Spatial Pattern

- Computed class specific covariance matrices \( \Sigma_1 \) and \( \Sigma_2 \)
- Solved the generalized eigenproblem

  $$
  \Sigma_1\, w = \lambda\, \Sigma_2\, w
  $$

  which is equivalent to maximizing the Rayleigh quotient

  $$
  w^\* = \arg\max_w \frac{w^\top \Sigma_1 w}{w^\top \Sigma_2 w}
  $$

- Derived spatial filters that maximize variance for one motor imagery class while minimizing it for the other
- Projected signals, computed log variance features in the \(\mu/\beta\) bands (around 8–30 Hz), reduced dimensionality while keeping discriminative structure

## Classification pipeline

- Supervised classifiers: Linear Discriminant Analysis and Support Vector Machines on the CSP log variance features
- Mapped motor imagery patterns to commands (left, right, forward, stop)
- Optimized for low latency to support real time interaction

## Real time control and safety constraints

- Majority voting across consecutive windows
- Temporal smoothing of predicted classes
- Confidence thresholds before issuing movement commands
- Immediate stop overrides

These safeguards reduced unintended movements and improved stability under noisy conditions.

## Results

- Reliable classification of motor imagery tasks
- Improved separability through CSP based spatial filtering
- Stable real time command generation with fewer false activations
- CSP spatial filters localized to expected motor cortex regions and showed contralateral patterns for left/right imagery, which helped verify signal quality.

## Reflection

This project strengthened my foundation in signal processing, frequency domain analysis, linear algebra, and real time system integration. It highlighted the gap between algorithmic accuracy and real world usability: in assistive technologies reliability and safety come first. Working directly with neural signals reinforced the importance of principled preprocessing, careful feature extraction, and disciplined system design when translating mathematical methods into practical human machine interfaces.
