# SK8-house-price-prediction

## Project Overview

This project demonstrates an end to end machine learning workflow, starting from raw web data collection and progressing through feature engineering, modelling and evaluation.

The objective was to:

* Scrape historical house sale data from Rightmove for the SK8 postcode area
* Clean and structure semi structured web data
* Engineer meaningful features
* Build and compare regression models to estimate house prices

The final models were evaluated using RMSE and R², with performance plateauing at approximately R² = 0.57, highlighting the importance of feature richness in real estate modelling.

---

# Part 1: Web Scraping – Data Collection

Notebook: `rightmove_sk8_scraping.ipynb`

## Objective

To programmatically collect historical sale data for the SK8 postcode area directly from Rightmove house price pages.

## Tools Used

* Python
* requests
* BeautifulSoup
* Regular expressions
* pandas

## Key Capabilities Demonstrated

### 1. Robust Page Handling

* Implemented custom request headers to mimic browser behaviour
* Used polite sleep intervals to avoid overwhelming the server
* Implemented HTML hashing to detect duplicate pages and prevent repeated scraping

### 2. Structured Extraction from Semi Structured HTML

Extracted and parsed:

* Full address
* Postcode
* Sale price
* Sale date
* Property type
* Tenure
* Number of bedrooms

Regular expressions were used to reliably extract:

* UK postcodes
* Currency formatted prices
* Date strings
* Bedrooms and tenure combinations

### 3. Data Integrity Checks

* Page level duplicate detection
* Controlled pagination
* Consolidation into a structured pandas DataFrame

The result was a clean raw dataset ready for analysis and modelling.

---

# Part 2: Data Preparation and Feature Engineering

Notebook: `Analysis and Learning.ipynb`

## Dataset Overview

* 960 property transactions
* Years covered: 2024 and 2025
* Target variable: `last_sold_price`

## Feature Engineering

The following features were created and refined:

* `postcode_sector` extracted from full postcode
* `sale_year` and `sale_month` derived from sale date
* Bedrooms cleaned and median imputed
* Categorical variables standardised

## Preprocessing Strategy

A leakage safe workflow was implemented:

1. Train test split performed early
2. Imputation fit only on training data
3. One hot encoding fit only on training data
4. Scaling applied only where appropriate

This was implemented using:

* scikit learn Pipeline
* ColumnTransformer
* SimpleImputer
* OneHotEncoder
* StandardScaler

---

# Part 3: Modelling

Three regression models were compared:

* Linear Regression
* Random Forest Regressor
* XGBoost Regressor

## Results

All models achieved similar performance:

* R² ≈ 0.57
* RMSE ≈ £108,000

This outcome is meaningful.

When tree based models do not outperform linear regression, it typically indicates that the limitation lies in feature richness rather than model complexity.

---

# Key Insights

## 1. Feature Limitation

The dataset did not include:

* Floor area
* Number of bathrooms
* Property condition
* Plot size
* Transport proximity
* Neighbourhood level socio economic indicators

These features are typically strong predictors in housing models.

The plateau in performance highlights a key lesson:

Model sophistication cannot compensate for missing explanatory variables.

## 2. Importance of Clean Data Engineering

The project demonstrates:

* End to end web data acquisition
* Regex based parsing of real world HTML
* Structured feature extraction
* Leakage safe preprocessing
* Proper model comparison

---

# How to Run the Project

1. Run the scraping notebook to generate raw data
2. Run the analysis notebook for preprocessing and modelling
3. Adjust model hyperparameters if required
4. Use the trained pipeline to predict new property prices

---

# Future Improvements

* Incorporate property size data
* Add bathroom count
* Integrate external economic indicators
* Use more granular postcode geospatial encoding
* Implement cross validated hyperparameter tuning
* Introduce prediction intervals

---

# Skills Demonstrated

* Web scraping
* Data cleaning and transformation
* Feature engineering
* Leakage safe ML pipelines
* Regression modelling
* Model evaluation and interpretation
