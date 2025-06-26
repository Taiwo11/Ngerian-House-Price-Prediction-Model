# 🏠 Nigerian House Price Prediction Project

## 📑 Table of Contents
- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Tools Used](#tools-used)
- [Data Cleaning Steps](#data-cleaning-steps)
- [Exploratory Data Analysis (EDA)](#exploratory-data-analysis-eda)
- [Results and Findings](#results-and-findings)
- [Recommendations](#recommendations)
- [Limitations](#limitations)

---

## 📘 Project Overview

The Nigerian real estate market is growing rapidly, yet pricing remains inconsistent due to a lack of standardized valuation models.  
This project aims to build a *machine learning-based predictive model* that estimates house prices using historical property listing data from across Nigeria.

*Goal:*  
Help property buyers, sellers, and developers make *data-driven decisions* with reliable price estimates based on key property features.

---

## 📊 Data Sources

- nigeria_housing_dataset_messy.csv

---

## 🛠 Tools Used

### Programming Language
- Python 🐍

### Libraries
- *Data Processing & Analysis:*  
  pandas, numpy

- *Visualization:*  
  matplotlib, seaborn

- *Machine Learning & Modeling:*  
  scikit-learn, xgboost

- *Evaluation Metrics:*  
  sklearn.metrics (MAE, RMSE)

- *Web Deployment (Optional):*  
  Streamlit (for interactive model deployment)

---

## 🧹 Data Cleaning Steps

1. *Initial Inspection*  
   - Used .shape, .head(), .info(), .isna() to inspect dataset

2. *Handling Missing Data*  
   - Dropped missing rows with df.dropna()

3. *Cleaning Price Column*  
   - Removed currency symbols (₦, commas), converted to numeric using .str.replace() and pd.to_numeric()

4. *Categorical Column Standardization*  
   - Columns like Has_Generator, Has_Borehole, Gated_Estate cleaned by converting to lowercase and replacing inconsistent labels

5. *Outlier Removal using IQR*  
   - Removed outliers in Listed_Price_NGN, Size_in_sq_m, Bedrooms, Bathrooms

6. *KMeans Clustering* (if enough data)  
   - Clustered properties into:  
     Budget, Standard, Premium, Luxury

7. *Encoding Categorical Variables*  
   - Applied pd.get_dummies() for one-hot encoding

8. *Final Dataset*  
   - Cleaned and prepared for clustering, visualization, and predictive modeling

---

## ❓ Exploratory Data Analysis (EDA)

We explored the dataset to answer questions such as:

1. What is the average listing price of properties?
2. Which cities/neighborhoods are most expensive?
3. Do more bedrooms/bathrooms lead to higher prices?
4. Do generators or boreholes increase value?
5. Are gated estates consistently higher priced?
6. What are the dominant features for each cluster?
7. Can price per square meter explain regional variation?
8. Can we segment properties into price tiers?
9. How does property size affect pricing?
10. What features best predict price?
11. Are any features redundant?
12. Which features are most important to buyers?

---
## 📊 Data Analysis

This section provides an overview of the initial data inspection and highlights interesting features worked with during exploration and modeling.

### 🔹 Loading the Dataset

We started by importing the necessary library and reading the dataset:

```python
import pandas as pd

# Load dataset
df = pd.read_csv("nigeria_housing_dataset_messy.csv")

print("Original shape:", df.shape)
print("\nFirst few rows:")
print(df.head())
```

## 📊 Results and Findings

- *Average listed price:* ₦55,929,510  
- *Cleaned dataset size:* Reduced from 1050 → 932 rows  
- *Missing/Inconsistent data:* ~11.24%

### 📉 Clustering
- Properties grouped into 4 clusters:
  - Cluster 0: Budget
  - Cluster 1: Standard
  - Cluster 2: Premium
  - Cluster 3: Luxury

### 🔍 Model Results

| Model             | MAE (₦)       | RMSE (₦)       |
|------------------|---------------|----------------|
| Random Forest     | 10,983,081.61 | 14,997,725.02  |
| Tuned RF          | 11,135,045.71 | 15,143,192.40  |
| XGBoost           | 11,521,972.94 | 15,182,831.23  |
| Linear Regression | 12,044,680.81 | 15,877,942.73  |

➡ *Best Model:* Default Random Forest (lowest MAE)

### 🔑 Top Predictive Features
- Size in sq m  
- Number of Bedrooms  
- Bathrooms  
- Location  
- Gated Estate  
- Generator Availability  

---

## ✅ Recommendations

- Standardize numerical features (e.g., size, bedrooms)
- Investigate outliers or unrealistic entries
- Carefully handle missing data (drop or impute)
- Use geographic encoding (e.g., cluster neighborhoods)
- Introduce price_per_sqm as a derived feature
- Expand dataset with more diverse and recent listings
- Incorporate timestamps for time series analysis
- Use interactive maps for visual exploration of listings

---

## ⚠ Limitations

1. *Small Dataset Size*  
   < 1000 rows after cleaning

2. *No Geographic Coordinates*  
   Limits precise spatial analysis

3. *Data Quality Issues*  
   Inconsistent formatting and missing labels

4. *Missing Features*  
   No data on property age, condition, proximity to infrastructure

5. *Remaining Outliers*  
   Some unrealistic prices still present

6. *Sampling Bias*  
   Uneven coverage across Nigerian states

7. *Black-box Modeling*  
   Tree models less interpretable than linear models

8. *No Date Column*  
   Prevents time trend or seasonal analysis

9. *Static Dataset*  
   Model not retrained with new data

10. *Market Drift*  
   Predictions may become outdated as real estate trends evolve

---

## 📂 Project Status
✅ Completed core predictive modeling  
📊 EDA and Clustering performed  
🌐 Optional Web Deployment pending

---

> Created with ❤ using Python and Machine Learning  
> For questions, feel free to open an issue or contact the maintainer.
