---
title: "Unsupervised Modeling of Long Horizon Behavioral Time Series"
date: 2022-05-01
featured_image: "/images/mental-health.jpg"
omit_header_text: true
description: "Built unsupervised time series pipelines to identify recurring long term trajectory patterns in irregular multi channel behavioral data using DTW, representation learning, and density based clustering."
summary: "Unsupervised time series models that surface long horizon trajectories and clusters from irregular behavioral data."
math: true
---


I worked on modeling long horizon behavioral time series using unsupervised learning methods. The objective was to understand how risk evolves over extended periods and to identify recurring temporal patterns without relying on predefined labels.

## Problem: risk develops gradually in longitudinal data

In many monitoring settings, risk does not appear suddenly; it develops through gradual changes across multiple signals observed over time. Data often contain continuous and discrete signals collected at different intervals, with irregular, incomplete, and heterogeneous records across individuals.

Central question: can we identify consistent long term trajectory patterns from irregular multi channel time series without supervised labels?

## Data structure

Multi year longitudinal records with continuous and discrete observations at different resolutions, including periodic self reports, continuous sensor data, event logs, and categorical observations.

Challenges: mixed sampling frequencies, missing values, variable follow up duration, and different scales across individuals.

## Preprocessing and standardization

- Temporal alignment across channels  
- Resampling strategies for mixed frequency data  
- Per individual normalization and detrending  
- Short gap imputation  
- Windowing to standardize analysis horizons  

Feature engineering:

- Event frequency and rate of change over time  
- Variability metrics  
- Persistence and streak length measures  
- Rolling window statistics  
- Lag based trend indicators  

## Distance based trajectory clustering

- Dynamic Time Warping to align sequences that evolve at different speeds  
  ![Dynamic Time Warping](/images/dtw.png)
- DTW distance computed as:
  
  $$
  \operatorname{DTW}(X, Y) = \min_{\pi} \sum_{(i,j) \in \pi} \lVert x_i - y_j \rVert^2
  $$
- Agglomerative and k medoids clustering  
- DTW barycenter averaging to compute representative prototypes  
  
  $$
  Z^\* = \arg\min_Z \sum_k \operatorname{DTW}(Z, X_k)^2
  $$
- Shapelet discovery to detect recurring short motifs  

## Representation learning for temporal embeddings

- Sequence autoencoders and temporal convolutional networks  
- InceptionTime for multi scale pattern extraction  
- Temporal Fusion Transformers for missingness and covariates  
- Contrastive pretraining for robust embeddings  
- HDBSCAN to cluster embeddings without fixing cluster counts  
- Exploratory generative sequence modeling to simulate alternative dynamics  

## Evaluation

- Silhouette scores, stability under resampling, agreement across approaches  
- Manual review for temporal coherence and structural consistency; clusters lacking consistent structure were discarded  

## Observations

- Recurring long horizon trajectory patterns  
- Distinct temporal evolution behaviors  
- Early signal motifs preceding larger shifts  
- Subgroups with stable long term dynamics  

## Reflection

Many real world risks evolve gradually and live in temporal structure rather than static snapshots. Modeling long horizon dynamics requires careful handling of mixed continuous and discrete data, alignment across variable sampling, robust similarity measures, and representation learning for complex temporal structure. It strengthened my interest in discovering latent structure where the objective is insight into dynamics rather than short term prediction alone.
