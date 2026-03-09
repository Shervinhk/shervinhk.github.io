---
title: "Mechanistic Modeling of Renal Drug Response"
date: 2024-01-01
featured_image: "/images/pub1.png"
omit_header_text: true
description: "Built a steady state nephron model that includes calcium and magnesium transport to study how drug induced transporter changes alter electrolyte balance along the kidney."
summary: "Steady state nephron model with calcium and magnesium transport to study drug effects on electrolyte balance."
---

During my M.Math at the University of Waterloo I built a physics based computational model of kidney function at the nephron level. The nephron is the functional unit of the kidney. By modeling transport along a representative nephron and enforcing physiological constraints we constructed a model intended to reflect whole kidney behavior in steady state. The goal was to study electrolyte regulation and the impact of medications on solute handling.

**Repository**
[https://github.com/Layton-Lab/nephron-calcium](https://github.com/Layton-Lab/nephron-calcium)


---

## Problem: Existing Kidney Models Ignored the Very Electrolytes Most Affected by Modern Diabetes Therapies

The kidney tightly regulates sodium calcium magnesium water and other solutes through coordinated transport across specialized nephron segments. Disturbances in this regulation can have systemic consequences.

Most existing whole nephron models focused primarily on sodium glucose and water. Calcium and magnesium transport were either simplified or omitted across segments. Because of this they could not adequately reflect how medications influence mineral balance.

The importance of calcium and magnesium became clear while analyzing the largest diabetes dataset in Canada. Using machine learning models and longitudinal analysis we observed persistent calcium and magnesium deficiencies in a substantial subset of patients. We also applied causal inference techniques such as propensity score matching to control for confounding and compare treated and untreated groups. These analyses suggested associations between certain diabetes therapies and downstream mineral imbalance.

Reduced calcium reabsorption can contribute to bone loss and osteoporosis particularly in patients treated with metformin or SGLT2 inhibitors. Magnesium dysregulation is associated with cardiovascular complications metabolic instability and neuromuscular effects.

We wanted to build a kidney model that explicitly captured these ions and provided a framework for evaluating both current and future medications. A mechanistic model makes it possible to identify which nephron segments are most affected by a given perturbation. Clinical trials measure overall outcomes but cannot isolate segment specific transport dynamics.

---

## How We Built a Physics Based Kidney Model From First Principles

We divided a representative nephron into its physiologically relevant segments including proximal tubule descending limb ascending limb distal tubule and collecting duct.

For each segment we wrote physics based transport equations for sodium calcium magnesium chloride glucose and other solutes. These equations were derived from conservation principles and established epithelial transport laws.

For each epithelial compartment we specified:

Mass conservation for every solute  
Electrochemical driving forces derived from membrane potentials  
Transcellular fluxes through known transporters  
Paracellular transport pathways  
Segment specific transporter densities based on experimental data

Each segment was constructed individually and then connected to adjacent segments through continuity conditions. By enforcing conservation and electrochemical balance across the full nephron we obtained an integrated kidney model at steady state.

![Nephron_all diagram](/images/Nepthon_all.gif)

---

## Reformulating a Large PDE System Into a Solvable Nonlinear ODE Problem

In principle the full spatial and temporal formulation would yield a large system of coupled partial differential equations over space and time. Solving such a system directly would be computationally expensive and difficult to analyze.

Instead we assumed steady state transport. By removing the time dimension the model reduces to a structured nonlinear system of ordinary differential equations and algebraic constraints. We solved this system using Newton's method.

This reformulation preserved mechanistic detail while making the problem computationally tractable.

---

## What the Model Revealed and How We Validated It

We developed a whole nephron kidney model explicitly incorporating calcium and magnesium transport.

We simulated pharmacological inhibition and evaluated its impact on electrolyte balance. The model allowed us to track how local transporter changes propagate downstream across segments.

We compared model predictions with published clinical studies and observed qualitative agreement in electrolyte trends under drug inhibition. This validation increased confidence that the model captures key physiological mechanisms.

The framework provides a controlled computational setting to study causal pathways that are difficult to isolate experimentally.

---

## Reflection

This project connected data driven analysis with mechanistic modeling. Machine learning and longitudinal methods surfaced patterns in real patient populations. Causal techniques such as propensity score matching strengthened the evidence that medication exposure may influence mineral balance. The mechanistic kidney model then provided a structured way to explore how those associations could arise from underlying transport dynamics.

Writing down the physics forces clarity. Every flux must balance and every constraint must hold.

This work strengthened my interest in combining mechanistic physiological models with statistical learning and causal inference to better understand complex human systems.
