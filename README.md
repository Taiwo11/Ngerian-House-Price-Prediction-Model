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

- [nigeria_housing_dataset_messy.csv](http://localhost:8888/files/AltSchool%20Africa%20KARATU24/My%20AltSchool%20Lecture%20Folder/DISU%20TAIYE%20PROJECTS/nigeria_housing_dataset_messy.csv?_xsrf=2%7Ce2b8daf1%7C3728c7bcacc6d31497f7e4ab2d2c2826%7C1752047970)

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
   - Cleaned and prepared for clustering, visualization, and predictive modeling [Here](http://localhost:8888/files/AltSchool%20Africa%20KARATU24/My%20AltSchool%20Lecture%20Folder/DISU%20TAIYE%20PROJECTS/clean_nigeria_housing.csv?_xsrf=2%7Ce2b8daf1%7C3728c7bcacc6d31497f7e4ab2d2c2826%7C1752047970)

---

## ❓ Exploratory Data Analysis (EDA)

We explored the dataset to answer questions such as:

1. What is the average listing price of properties?
2. Which neighborhoods are most expensive?![Screenshot 2025-07-09 110458](https://github.com/user-attachments/assets/8b8bd265-6e29-4e8f-b43c-e4df63aae49e)
3. Do more bedrooms/bathrooms lead to higher prices?
4. Do generators or boreholes increase value?
5. Are gated estates consistently higher priced?
6. What are the dominant features for each cluster?![Screenshot 2025-07-09 131806](https://github.com/user-attachments/assets/a2290f76-50a3-4dbf-9937-ebbc006376f1)
7. Can price per square meter explain regional variation?![Screenshot 2025-07-09 110926](https://github.com/user-attachments/assets/6da18201-a151-4b70-a92a-6fe095a47b68)
8. Can we segment properties into price tiers?![Screenshot 2025-07-09 111542](https://github.com/user-attachments/assets/3417b4b4-189e-4b9b-8398-714dc0df7f4e)
9. How does property size affect pricing?![Screenshot 2025-07-09 111718](https://github.com/user-attachments/assets/4a66797d-dc77-4187-b89b-5429f6a4c414)
10. What features best predict price?![Screenshot 2025-07-09 131932](https://github.com/user-attachments/assets/a0e81dae-f1f0-4abb-b215-7a3e4d18f256)
11. Are any features redundant?![Screenshot 2025-07-09 112815](https://github.com/user-attachments/assets/b4371638-104e-4895-b242-86bb0e1107b1)
12. Which features are most important to buyers?
13. What is the relationship between property size and price across cities?![Screenshot 2025-07-09 112854](https://github.com/user-attachments/assets/96477072-f0d5-4e6e-8630-12df64883e91)

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

- *Average listed price:* ₦55,929,511
- Yes, more bedrooms/bathrooms lead to higher prices
- Boreholeand Generators increases value
- Gated Estates are not higher priced
- *Cleaned dataset size:* Reduced from 1050 → 932 rows  
- *Missing/Inconsistent data:* ~11.24%
- Features with correlation above 0.9 can be considered redundant
- Yes(Check correlation)
- Based on correlation and price impact:
	•	Bedrooms, Bathrooms, Size
	•	Location (City/Neighborhood)
	•	Amenities (Gated Estate, Generator, Borehole)
These influence both listing price and buyer interest

### 📉 Clustering
- Properties grouped into 4 clusters:
  - Cluster 0: Budget
  - Cluster 1: Standard
  - Cluster 2: Premium
  - Cluster 3: Luxury

### 🔍 Model Results (Updated)

| Model              | MAE (₦)           | RMSE (₦)          |
|--------------------|-------------------|-------------------|
| Random Forest      | ₦1,798,849.90     | ₦2,988,053.51     |
| Tuned RF           | ₦1,711,718.46     | ₦2,862,242.98     |
| XGBoost            | ₦1,654,691.50     | ₦2,595,829.89     |
| Linear Regression  | ₦5,067,100.42     | ₦6,933,812.33     |

➡ *Best Model:* ✅ *XGBoost* — lowest MAE and RMSE overall.

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
🌐 Web Deployment pending

---

> Created with ❤ using Python and Machine Learning  
> For questions, feel free to open an issue or contact the maintainer.
