# Predicting Physics Observables with LHC Data  
### Prompt vs Non-Prompt D* Meson Classification using Machine Learning

## Overview

This repository contains a complete end-to-end analysis for classifying  
$\mathrm{D}^{*+} \rightarrow \mathrm{D}^0 \pi^+\$ candidates into **prompt**, **non-prompt**, and **background** categories using **topological variables** derived from LHC data.

The project combines **physics-motivated feature selection** with **machine learning (BDT)** techniques, following workflows commonly used in modern high-energy physics experiments.

---

## Physics Motivation

At the LHC, D* mesons can be produced via:
- **Prompt production** (direct charm hadronization at the primary vertex),
- **Non-prompt production** (from displaced B-hadron decays),
- **Combinatorial background** (random track combinations).

Separating these components is crucial for:
- charm production measurements,
- feed-down subtraction,
- precision heavy-flavor physics.

This project focuses on using **decay topology alone**, closely mirroring real experimental analyses.

---


---

## Dataset Description

Three ROOT files are used:
- `Prompt_DstarToD0Pi.root`
- `Nonprompt_DstarToD0Pi.root`
- `Bkg_DstarToD0Pi.root`

Each file contains a TTree named `treeMLDstar`.  
Each entry corresponds to a **reconstructed D\*** candidate (not a collision event).

---

## Features Used

### Topological Variables (used for training)
- `fCpaD0`
- `fCpaXYD0`
- `fDecayLengthXYD0`
- `fImpactParameterProductD0`
- `fImpParamSoftPi`
- `fMaxNormalisedDeltaIPD0`

These variables encode:
- decay displacement,
- pointing geometry,
- impact parameters of decay products.

### Kinematic Variables (not used for training)
- `fPt`
- `fM`
- `fMD0`
- `fInvDeltaMass`

These are studied for validation and interpretation only, to avoid bias.

---

## Machine Learning Methodology

- **Model**: Boosted Decision Tree (XGBoost)
- **Task**: Multi-class classification  
  (Background / Non-prompt / Prompt)
- **Train/Test split**: 70% / 30%
- **Transverse momentum range**:
  $
  6 < p_{\mathrm{T}} < 8\ \text{GeV}/c
  $

Exploratory data analysis and correlation studies are performed before training.

---

## Performance Evaluation

Model performance is evaluated using **ROC curves**, standard in HEP analyses.

### Key results:
- **Prompt vs Background**: AUC ≈ **0.961**
- **Prompt vs Non-Prompt**: AUC ≈ **0.881**

A physics-motivated working point is chosen:
- Prompt efficiency ≈ **85%**
- Background efficiency ≈ **6.5%**
- Non-prompt efficiency ≈ **30%**

This provides strong background rejection while retaining most prompt signal.

---

## Analysis Workflow

1. Inspect ROOT files and branches
2. Select pT range and candidate samples
3. Perform exploratory data analysis (EDA)
4. Study correlations between variables
5. Train multi-class BDT
6. Evaluate with ROC curves
7. Select a physics-motivated working point

All steps are documented in detail in the accompanying report.

---

## Documentation

A detailed **LaTeX report (PDF)** is included, covering:
- physics background,
- decay topology and vertexing,
- variable definitions,
- ML methodology,
- mathematical definitions of performance metrics,
- interpretation of results.

The report is written to be accessible even to readers new to ML in particle physics.

---

## Tools and Libraries

- ROOT / uproot
- NumPy, Pandas
- Matplotlib
- Scikit-learn
- XGBoost
- LaTeX

---

## Future Extensions

- Testing on mixed (unknown-class) samples
- Inclusion of PID (Particle Identification) variables
- Training across multiple pT bins
- Systematic uncertainty studies

---

## Author

**Kain Shivendra**  
Engineering Physics  
Indian Institute of Technology Bombay




