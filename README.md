# Bayesian Linear Regression on California Housing Dataset

## 📌 Overview

This project implements a **Bayesian Linear Regression model** using PyMC on the California Housing dataset. The goal is to move beyond point estimates and capture **uncertainty in predictions**, followed by a rigorous **Bayesian model criticism workflow**.

---

## ⚙️ Model Description

* Likelihood: Gaussian
* Priors: Weakly informative priors on coefficients
* Inference: NUTS (Hamiltonian Monte Carlo)
* Framework: PyMC + ArviZ

---

## 🚀 Workflow

1. Data preprocessing and scaling
2. Model specification
3. Posterior sampling using NUTS
4. Posterior predictive sampling
5. Model evaluation and criticism

---

## 📊 Results

* The model successfully learns relationships between features and house prices
* Posterior distributions provide uncertainty estimates for all parameters
* Predictions are reasonable but show limitations in capturing complex patterns

---

# 🔍 Bayesian Model Criticism

This section evaluates how well the model represents the data-generating process.

---

## 1. Posterior Predictive Checks (PPC)

Posterior predictive samples were generated and compared against the observed data.

### Observations:

* The overall distribution of simulated data roughly matches the real data
* Mean predictions are close to observed values
* However, discrepancies appear in the **tails of the distribution**, indicating the model struggles with extreme house prices

👉 **Conclusion:**
The model captures central tendencies but fails to fully represent variability in the data.

---

## 2. Residual Analysis

Residuals were computed as:

residual = y_true - y_pred

### Observations:

* Residual plots show **structured patterns**, not purely random scatter
* Evidence of **non-linearity** in the relationship between features and target
* Variance of residuals is not constant (heteroscedasticity)

👉 **Conclusion:**
The linearity assumption is violated, and the model is likely underfitting complex relationships.

---

## 3. Normality of Residuals

A Q-Q plot was used to compare residuals with a normal distribution.

### Observations:

* Residuals deviate from normality, especially in the tails
* Indicates presence of **outliers or heavy-tailed behavior**

👉 **Conclusion:**
The Gaussian likelihood assumption may not be appropriate.

---

## 4. Predictive Uncertainty Calibration

95% credible intervals were computed for predictions.

### Observations:

* Coverage is not close to the expected 95%
* Some true values fall outside predicted intervals
* Indicates **miscalibrated uncertainty**

👉 **Conclusion:**
The model is either overconfident or underconfident in different regions.

---

## 5. WAIC / LOO (Out-of-Sample Performance)

Leave-One-Out cross-validation was used to estimate predictive performance.

### Observations:

* LOO reveals variability in predictive accuracy across data points
* Some observations have high influence (high k-hat values)

👉 **Conclusion:**
Certain data points are not well explained by the model, indicating **model misspecification**.

---

## ⚠️ Key Limitations Identified

1. **Linearity assumption is too restrictive**
2. **Homoscedastic noise assumption is violated**
3. **Gaussian likelihood does not capture heavy tails**
4. Model struggles with extreme values and complex interactions

---

## 🔧 Potential Improvements

Based on model criticism:

* Introduce **non-linear features** (polynomial terms or splines)
* Use **heteroscedastic models** (variance as a function of inputs)
* Replace Gaussian likelihood with **Student-T distribution**
* Explore **Gaussian Processes** for flexible function modeling

---

## 🧠 Key Takeaway

This project demonstrates that:

> Building a Bayesian model is only the first step —
> **understanding where it fails is what makes it valuable.**

---

## 📁 Future Work

* Extend to hierarchical models
* Explore spatial modeling (relevant for real estate data)
* Compare multiple Bayesian models using LOO

---

## 🛠️ Tech Stack

* Python
* PyMC
* ArviZ
* NumPy / SciPy / Matplotlib

---

## 🙌 Acknowledgment

This project is part of my preparation for contributing to Bayesian modeling and probabilistic programming projects.

---








































# Bayesian Linear Regression with PyMC

## Overview

This project implements a **Bayesian Linear Regression model** using the Python probabilistic programming framework **PyMC**. The goal of this project was to build a strong conceptual understanding of the Bayesian modeling workflow, posterior inference, and model evaluation before moving toward more advanced models such as hierarchical models, Gaussian processes, and spatial models.

The model is trained on the California Housing dataset and demonstrates the full Bayesian workflow:

1. Data exploration and preprocessing
2. Bayesian model specification
3. Posterior inference using MCMC sampling
4. Posterior predictive checks
5. Out-of-sample prediction and evaluation

This repository is part of my preparation for contributing to PyMC and eventually working on spatial modeling algorithms.

---

# Dataset

The model uses the **California Housing dataset** provided through the scikit-learn library.

Target variable:

* Median house value

Selected features:

* Median Income
* House Age
* Average Rooms
* Latitude

These features were chosen after performing exploratory data analysis and examining correlations with the target variable.

---

# Bayesian Model

The regression model assumes that house prices are generated from a linear relationship with Gaussian noise.

### Linear Model

[
y = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + \beta_3 x_3 + \beta_4 x_4 + \epsilon
]

where

* (y) is the house price
* (x_i) are the input features
* (\beta_i) are regression coefficients
* (\epsilon) represents Gaussian noise

---

# Priors

The Bayesian model specifies prior distributions over the parameters.

Intercept:

Normal distribution centered near the mean house price.

Coefficients:

Normal priors centered at zero representing weak prior belief about feature influence.

Noise parameter:

Half-Normal distribution ensuring the standard deviation remains positive.

These priors are intentionally **weakly informative**, allowing the data to dominate posterior inference.

---

# Likelihood

The likelihood assumes that observed house prices are normally distributed around the linear prediction.

[
y \sim \text{Normal}(\mu, \sigma)
]

where

[
\mu = \beta_0 + \beta_1 x_1 + ... + \beta_p x_p
]

---

# Posterior Inference

Posterior inference is performed using **Markov Chain Monte Carlo (MCMC)** sampling.

Specifically, PyMC uses the **No-U-Turn Sampler (NUTS)**, an adaptive variant of Hamiltonian Monte Carlo.

The sampling process estimates the posterior distribution:

[
p(\beta, \sigma \mid X, y)
]

which represents the uncertainty in model parameters after observing the data.

---

# Workflow

The modeling workflow implemented in this repository follows these steps:

1. Exploratory Data Analysis
2. Feature selection
3. Train-test split
4. Feature scaling
5. Bayesian model construction
6. Posterior sampling
7. Posterior diagnostics
8. Posterior predictive checks
9. Out-of-sample prediction

---

# Model Diagnostics

Several diagnostics were used to ensure the quality of the posterior samples.

Trace plots
Used to visually inspect sampling convergence.

R-hat statistic
Ensures chains have converged to the same posterior distribution.

Posterior predictive checks
Verify whether simulated data from the model resembles the observed data.

---

# Out-of-Sample Prediction

After fitting the model, predictions were generated on a held-out test dataset using PyMC’s `set_data()` functionality.

The predictive performance was evaluated using:

R² score

This step demonstrates how Bayesian models can be used for predictive tasks while still providing uncertainty estimates.

---

# Key Learnings

This project helped develop a deeper understanding of the Bayesian modeling workflow:

### 1. Structure of a Bayesian Model

A probabilistic model is defined using three components:

* Prior distributions
* Likelihood function
* Posterior inference

### 2. Posterior Sampling

PyMC constructs the **log posterior function** and uses gradient-based samplers (NUTS/HMC) to explore the parameter space efficiently.

### 3. Uncertainty Quantification

Unlike classical regression, Bayesian regression produces **distributions over parameters**, allowing us to measure uncertainty in coefficient estimates.

### 4. Posterior Predictive Modeling

Once the posterior distribution is obtained, new predictions can be generated by integrating over parameter uncertainty.

### 5. Importance of Model Diagnostics

Convergence diagnostics and posterior predictive checks are critical to ensure that the model represents the data well.

---

# Repository Structure

```
bayesian-housing-regression/
│
├── code.ipynb
│   Bayesian regression implementation
│
├── README.md
│   Project documentation
│
└── requirements.txt
│   Python dependencies
```

---

# Future Work

The long-term goal of this project is to build toward more advanced probabilistic models used in spatial statistics.

Planned next steps include:

* Hierarchical Bayesian models
* Gaussian Processes
* Spatial regression models
* Spatio-temporal modeling

These methods are widely used in geostatistics, epidemiology, and environmental modeling.

---

# Technologies Used

Python
NumPy
Pandas
Matplotlib
Scikit-learn
PyMC
ArviZ

---

# Motivation

This project is part of my preparation to contribute to the PyMC ecosystem and to develop a deeper understanding of probabilistic modeling and Bayesian inference.

---

# References

PyMC documentation
Bayesian Data Analysis – Gelman et al.
Statistical Rethinking – Richard McElreath
