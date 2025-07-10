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

Average listed price: *₦55,929,511*

2. Which neighborhoods are most expensive?
![Screenshot 2025-07-09 110458](https://github.com/user-attachments/assets/8b8bd265-6e29-4e8f-b43c-e4df63aae49e)

Based on the average listed prices, the most expensive neighborhoods in the dataset include:
- *Ikeja*
- *Gwarinpa*
- *Maitama*
- *Rumuola*
- *Trans-Amadi*
- 
These areas have average property prices close to or above ₦60 million. Properties in these neighborhoods command premium prices, likely due to location, infrastructure, or demand.

3. Do generators, boreholes or gated estates increase value?

*Generators:*  
✅ Yes — properties with generators have *higher average prices*, showing that buyers value backup power.

*Gated Estates:*  
❌ No — surprisingly, being in a gated estate does *not significantly increase price* in this dataset.

*Boreholes:*

✅ Yes — properties with boreholes have *higher average prices*, showing that buyers value access to water.

💡 *Insight:*  
 Power reliability (generators) and water access are seen as premiun amenities, they boosts property value, while gated estates may not offer a pricing premium possibly because it's a common feature or not tied to luxury level in this market.

4. Can price per square meter explain regional variation?

Yes, price per square meter does vary across regions, as shown in the chart below. On average:

• Lagos properties are priced around ₦490,000 per square meter

• Abuja averages ₦470,000 per square meter

• Port Harcourt is slightly higher, close to ₦495,000 per square meter

Although the prices are relatively close, the slight variations reflect differences in demand and urban infrastructure. For example, Lagos remains a top real estate market due to its population size and commercial activity, while Port Harcourt may have higher prices due to fewer available premium properties in central areas.
![Screenshot 2025-07-09 110926](https://github.com/user-attachments/assets/6da18201-a151-4b70-a92a-6fe095a47b68)

5. Can we segment properties into price tiers?![Screenshot 2025-07-09 111542](https://github.com/user-attachments/assets/3417b4b4-189e-4b9b-8398-714dc0df7f4e)

*Distinct Price Tiers Identified:*
- *Premium Properties* (~₦23M) — Lowest volume, exclusive
- *Luxury Properties* (~₦48M) — High-end, fewer listings
- *Budget Properties* (~₦67M) — Affordable, growing segment
- *Standard Properties* (~₦112M) — Most common in market

6. What are the dominant features for each cluster?
 *Inferred Cluster Characteristics:*
- *Standard:* Mid-size (100–200 sqm), typical amenities, general locations
- *Budget:* Smaller (<100 sqm), basic features, affordable areas
- *Luxury:* Larger (200+ sqm), premium zones, upscale features
- *Premium:* Ultra-exclusive, highest price per sqm, rare listings

💡 *Note:*  
 Clusters are based on pricing patterns; for exact feature drivers, see clustering variables (size, location, amenities, etc.).

 7. How does property size affect pricing?![Screenshot 2025-07-09 111718](https://github.com/user-attachments/assets/4a66797d-dc77-4187-b89b-5429f6a4c414)

*Clear Size-Price Trend:*
- Properties under 50 sqm have the lowest prices (~₦17M)
- Prices steadily rise with size, peaking at 250+ sqm (~₦110M)
 *Price Progression by Size Band:*
- *<50 sqm*: Lowest tier  
- *50–100 sqm*: Moderate increase  
- *100–150 sqm*: Upward trend  
- *150–200 sqm*: Significant jump  
- *200–250 sqm*: High range  
- *250+ sqm*: Premium pricing

💡 *Insight:*  
 Pricing increases almost linearly with size. Larger homes (200+ sqm) command *disproportionately higher prices*, reflecting buyer preference for space, luxury, and investment potential.
 
 8. Are any features redundant?

Yes, some features in the dataset are strongly correlated looking at the heatmap below, meaning they carry similar information. For example:
- *Bedrooms and Bathrooms* have a very high correlation of *0.96*
- *Bedrooms and Size in square meters* also correlate strongly at *0.85*

This means that if we know how many bedrooms a house has, we can usually guess the number of bathrooms or the overall size quite accurately. These features are considered *redundant* because they move together, including all of them in a model might not add much value and could even lead to confusion.

📌 Simple explanation:  
 If two features always move together, you don’t always need to use both in prediction.

![Screenshot 2025-07-09 112815](https://github.com/user-attachments/assets/b4371638-104e-4895-b242-86bb0e1107b1)

9. Which features are most important to buyers?

From the correlation heatmap above, the following features are most strongly related to price:
- *Size in square meters* → correlation of *0.87*
- *Bedrooms* → correlation of *0.75*
- *Bathrooms* → correlation of *0.72*
These strong positive correlations suggest that *larger homes with more rooms tend to cost more*, which makes sense from a buyer’s perspective.

Interestingly:
- *Year Built* has a very weak correlation with price (~0.01*), meaning buyers **don’t seem to care much whether a house is new or old* , space and room count matter more.
📌 Key takeaway:  
 Buyers are mostly paying for *space and rooms*, not age of the house.

10. What features best predict price?

Based on the correlation heatmap above, the feature that best predicts property price is:

- **Size in square meters (Size_in_sq_m)** → correlation of *0.87* with price

This means that property size has the *strongest relationship* with the listed price, the larger the home the more expensive it tends to be.

Other features like:
- *Bedrooms* (0.75) and
- *Bathrooms* (0.72)

also influence price, but not as strongly as size.

🧠 Key insight:  
 Bigger houses tend to cost more and size is the best single predictor of price in this dataset.
 
11. Do larger properties tend to cost more?

Yes, the heatmap shows a strong positive correlation of *0.87* between property size (Size_in_sq_m) and price (Listed_Price_NGN). 

This means that, in general, *the larger the property, the higher the price*.

🧠 Key takeaway:  
 Bigger houses = bigger price tag.
 
 12. Do more bedrooms/bathrooms lead to higher prices?

 *Yes, strongly.*  
- *Bedrooms vs. Price:* Correlation = *0.75*  
- *Bathrooms vs. Price:* Correlation = *0.72*

This indicates that properties with more bedrooms and bathrooms generally command higher prices.

💡 *Insight:*  
 Bedrooms and bathrooms are key value drivers, likely reflecting larger home sizes and better livability.
 
 13. What is the relationship between property size and price across cities?
     ![Screenshot 2025-07-09 112854](https://github.com/user-attachments/assets/96477072-f0d5-4e6e-8630-12df64883e91)

*Strong Size-Price Correlation:*
- Prices increase with property size across all cities (linear trend)
- Larger properties consistently command higher prices
🏙 *City-Based Variations:*
- Cities show distinct clusters on the scatter plot
- Some cities (premium markets) show higher prices even for smaller properties
- Others fall into more affordable price ranges
📐 *Distribution Overview:*
- Property sizes: 0–300+ sqm  
- Price range: ₦10M to ₦150M  
- Most properties fall between 50–200 sqm, priced ₦20M–₦120M

- 💡 *Insight:*  
 While size drives price, *location matters*, the same sized property can be much more expensive in a premium city.

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

- *Cleaned dataset size:* Reduced from 1050 → 932 rows  
- *Missing/Inconsistent data:* ~11.24%
- Features with correlation above 0.9 can be considered redundant
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
