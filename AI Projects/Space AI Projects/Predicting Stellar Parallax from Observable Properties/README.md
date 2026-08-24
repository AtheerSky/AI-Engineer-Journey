# Predicting Stellar Parallax from Gaia DR3 Data Using Machine Learning

> **What remains, when we cannot go back?**

Some moments leave only traces — a memory, a photograph, a small piece of what once existed.

The stars leave traces too. Because their light takes years to reach us, when we look at a star, we are also looking into its past.

That led to the question:

> **Can observable stellar properties tell us something about parallax?**

## Research Question

Gaia measures stellar parallax, allowing astronomers to estimate stellar distances.

This project asks:

> **Can we predict parallax from a star's brightness, colour, and sky position without using parallax itself as an input?**

## Method

Using **2 million Gaia DR3 stellar sources**, I:

* Cleaned the data based on measurement quality.
* Created leakage-safe features from brightness, colour, and sky position.
* Compared **Linear Regression, Random Forest, and XGBoost**.
* Used GPU-accelerated tools to handle the dataset.
* Evaluated the models using RMSE, R², and **5-fold cross-validation**.

## Results

**XGBoost performed best:**

* Test RMSE: **0.8003**
* Test R²: **0.1927**
* 5-fold CV RMSE: **0.7966 ± 0.0052**
* Tuned test RMSE: **0.7991**

The models learned a **real but limited signal**.

XGBoost relied most strongly on **colour**, while Random Forest gave the highest importance to an **engineered brightness** feature.

Parallax uncertainty also increases for fainter stars, helping explain why the predictive signal remained modest.

## Conclusion

Brightness, colour, and sky position contain information related to stellar parallax — but only part of the story.

Parallax is fundamentally a **geometric measurement**, while our features mainly describe how a star appears to us.

> **A trace never tells the whole story — but it can tell us something real.**
<img width="1103" height="590" alt="image" src="https://github.com/user-attachments/assets/eb7ce6c2-c0a0-43a6-b795-f3aa4d6025d3" />

