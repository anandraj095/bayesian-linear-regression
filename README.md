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