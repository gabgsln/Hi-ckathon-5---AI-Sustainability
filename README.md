 # Hi!ckathon #5 — AI & Sustainability

<p align="center">
  <img src="https://www.hi-paris.fr/wp-content/uploads/2020/09/logo-hi-paris-retina.png" width="300" height="200" />
</p>

<p align="center">
  <b>Team:</b> Yanis Montacer • Gabriel Gaslain • Gabriel Enthoven  
  <br/>
  <b>Track:</b> AI & Sustainability  
  <br/>
  <b>Result:</b> 🥉 3rd best score
</p>

---

## Overview

This repository contains our submission for **Hi!ckathon #5 (AI & Sustainability)**.  
We achieved the **3rd best score** with a deliberately **simple and robust pipeline**.

Instead of heavy feature engineering, we focused on:
- clean feature pruning,
- strong gradient boosting models,
- lightweight ensembling.

In this competition, **aggressive feature engineering wasn’t necessary** to reach top performance.

---

## Approach

### Models
We trained three complementary tree-based regressors:
- **XGBoost**
- **LightGBM**
- **CatBoost**

Each model was tuned with **Optuna** on a small tuning subset to keep experimentation fast and consistent.

### Ensemble Strategy

#### 1) Simple Blending
We tested weighted averages of the three models’ predictions.

#### 2) Ridge Stacking (Final)
Our best and most stable approach was **Ridge stacking**:
- Train XGBoost, LightGBM, and CatBoost as **base models**.
- Use their predictions as features for a **meta-model**.
- Fit a **Ridge regression** to learn optimal, regularized linear weights.

This keeps the ensemble:
- **simple**
- **interpretable**
- **less prone to overfitting** thanks to L2 regularization.

