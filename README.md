# Dimension Reduction Methods — Principal Component Analysis (PCA)

**Authors:** Banu Öven, Eyüp Erman Erman

## 1. Introduction and Matrix Selection

To reduce the dimensionality of the Customer Churn dataset while retaining maximum variance,
Principal Component Analysis (PCA) was performed.

The **Covariance Matrix** was first tested on unscaled data, but due to significant scale
differences between features (e.g. `Seconds of Use` vs. `Complains`), the unscaled covariance
matrix was biased toward high-magnitude features. For a scientifically valid dimensionality
reduction, the dataset was standardized (mean = 0, std = 1) and PCA was re-applied using the
**Correlation Matrix**.

## 2. Variance Thresholds (Covariance vs. Correlation)

### a) Covariance Matrix (unscaled data)

Because the data was not standardized, variables with massive numerical ranges dominated the
variance, producing highly skewed results:

| Variance Threshold | Components Required |
|---|---|
| 90% | 1 |
| 95% | 1 |
| 99% | 2 |

### b) Correlation Matrix (standardized data — scientifically accurate approach)

| Variance Threshold | Components Required |
|---|---|
| 90% | 7 |
| 95% | 9 |
| 99% | 10 |

**Variance explained by the first components (Correlation Matrix):**

- PC1 + PC2 together account for **48.75%** of total variability.
- PC1 + PC2 + PC3 together account for **61.37%** of total variability.

## 3. Mathematical Representation of the Components

The principal components are linear combinations of the standardized original variables
(X1–X13 correspond to `Call_Failure` through `Customer_Value`):

<img width="765" height="327" alt="02_eigenvector_formulas" src="https://github.com/user-attachments/assets/edc6f192-29cb-45ac-956a-e5ab8d8fb79e" />


```
PC1 = 0.317·X1 − 0.072·X2 + 0.064·X3 + 0.317·X4 + 0.434·X5 + 0.441·X6 + 0.186·X7
      + 0.391·X8 + 0.007·X9 + 0.176·X10 − 0.309·X11 + 0.006·X12 + 0.304·X13

PC2 = 0.186·X1 + 0.094·X2 + 0.036·X3 + 0.253·X4 + 0.061·X5 + 0.035·X6 − 0.330·X7
      + 0.090·X8 + 0.550·X9 − 0.133·X10 + 0.081·X11 + 0.559·X12 − 0.360·X13

PC3 = −0.309·X1 − 0.255·X2 − 0.066·X3 + 0.036·X4 − 0.140·X5 − 0.193·X6 + 0.522·X7
      − 0.162·X8 + 0.394·X9 + 0.004·X10 − 0.221·X11 + 0.375·X12 + 0.365·X13
```

## 4. PCA Visualizations

Points are colored by actual `Churn` status to assess spatial separability.

**2D PCA Scatter Plot** (PC1 vs. PC2):

<img width="1205" height="623" alt="01_2d_pca_scatter" src="https://github.com/user-attachments/assets/576d16eb-62c8-45b1-bc52-9f0613afd511" />


**3D PCA Scatter Plot** (PC1, PC2, PC3):

<img width="936" height="847" alt="03_3d_pca_scatter" src="https://github.com/user-attachments/assets/af5941ba-c0e8-4faf-b323-a4f1e3b29ca9" />


## 5. Conclusion and Discussion

PCA was successfully applied as a dimensionality reduction technique on the 13-dimensional
Customer Churn dataset. The comparison highlighted the necessity of the **Correlation Matrix**
over the Covariance Matrix to eliminate feature-scale bias and produce mathematically sound
components.

- PC1 + PC2 capture **48.75%** of total variance; PC1–PC3 expand this to **61.37%**.
- Although 61.37% variance retention means some information is discarded, the projection
  compresses the complex 13-dimensional space into a highly interpretable 3D structure.
- Features related to call frequency, seconds of use, and overall customer value have the
  highest absolute loadings on PC1, making them the primary drivers of variability.
- The 2D/3D scatter plots show spatial overlap between churn classes but still provide a
  cleaner framework for observing customer distributions than the raw feature space.

PCA offers an effective balance between data compression and information retention, serving
as a solid preprocessing step for subsequent predictive modeling, classification, or targeted
retention strategies.
