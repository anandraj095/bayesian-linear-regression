# Bayesian Modeling with PyMC

## 📌 Overview

This repository contains a collection of **Bayesian modeling experiments and prototypes** built using PyMC.  
The goal is to develop a strong understanding of probabilistic modeling, inference, and model criticism, while also exploring more advanced topics such as **spatial modeling (BYM2)**.

---

## 📂 Repository Structure

### 🔹 Core Bayesian Regression

- `01_gaussian_linear_regression.ipynb`  
  Bayesian Linear Regression with Gaussian likelihood on the California Housing dataset.

- `02_student_t_likelihood.ipynb`  
  Extension of the regression model using a **Student-T likelihood** to handle heavy-tailed noise and outliers.

---

### 🔹 Spatial Modeling Prototype (GSoC Preparation)

- `bym2_minimal_prototype.ipynb`  
  A minimal prototype of a **BYM2-style spatial model** using PyMC.

  This notebook demonstrates:
  - Structured + unstructured spatial decomposition
  - Use of ICAR priors for spatial dependence
  - Comparison with a baseline iid model
  - Basic validation on synthetic areal count data

  👉 This notebook was created as part of my **GSoC 2026 proposal for PyMC (Spatial Modeling)**.

---

## ⚙️ Tech Stack

- Python
- PyMC
- ArviZ
- NumPy / SciPy
- Matplotlib

---

## 🚀 Workflow (General)

Across notebooks, the typical workflow includes:

1. Data preprocessing and scaling  
2. Model specification  
3. Posterior sampling using NUTS (HMC)  
4. Posterior predictive checks  
5. Model evaluation and criticism  

---

## 🔍 Bayesian Model Criticism

The regression notebooks include a detailed model criticism workflow:

- Posterior Predictive Checks (PPC)
- Residual analysis
- Normality checks
- Predictive uncertainty calibration
- WAIC / LOO evaluation

### Key insights:

- Linear models fail to capture complex relationships  
- Residuals show heteroscedasticity and non-linearity  
- Gaussian likelihood struggles with heavy-tailed data  
- Predictive uncertainty may be miscalibrated  

---

## ⚠️ Key Learnings

- Bayesian modeling provides **uncertainty-aware predictions**
- Model assumptions must be **critically evaluated**
- Simple models often fail in **real-world settings**
- Spatial structure is important in many domains (e.g., housing, epidemiology)

---

## 🔧 Future Work

- Non-linear Bayesian models (splines / feature engineering)
- Heteroscedastic regression
- Gaussian Processes
- Hierarchical models
- **Full BYM2 implementation in PyMC (planned contribution)**

---

## 🧠 Motivation

This repository is part of my preparation for contributing to **probabilistic programming and Bayesian modeling projects**, particularly in the PyMC ecosystem.

---

## 🙌 Acknowledgment

Built as part of my learning journey in Bayesian statistics, probabilistic programming, and open-source contribution.