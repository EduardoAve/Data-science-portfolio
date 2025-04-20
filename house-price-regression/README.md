
## Project Overview

This project focuses on predicting the sale price of houses in Ames, Iowa, using the well-known Ames Housing dataset. It involves applying various regression techniques to model the relationship between numerous house features (physical characteristics, location, quality ratings, etc.) and their final sale price.

The project covers a comprehensive data science workflow, including:
* In-depth Exploratory Data Analysis (EDA)
* Data Cleaning and Preprocessing (handling missing values, feature transformations)
* Feature Engineering
* Training and evaluating multiple regression models (Linear, Regularized, Tree-based)
* Interpreting results and identifying key price drivers (based on EDA).

## Motivation

Predicting house prices accurately is a common and valuable task in the real estate industry and for homeowners. Understanding the factors that influence house prices helps buyers, sellers, and real estate professionals make informed decisions. This project aims to build a predictive model while exploring the complex interplay of features that determine a house's value.

## Data Source

* **Dataset:** Ames Housing dataset, prepared by Dean De Cock.
* **Source:** Kaggle Competition - "House Prices: Advanced Regression Techniques". Link: [https://www.kaggle.com/c/house-prices-advanced-regression-techniques](https://www.kaggle.com/c/house-prices-advanced-regression-techniques)
* **Files Used:**
    * `train.csv`: Contains the training data, including features and the target `SalePrice`.
    * `data_description.txt`: **Crucial file** explaining each column name and its meaning/values (used extensively for preprocessing decisions).
* **Loading Method:** The accompanying notebook (`house_price_regression.ipynb` - *adjust name if different*) uses manual file upload via the Google Colab interface for `train.csv`.

## Methodology

The project workflow involved the following steps:

1.  **Data Loading & Initial Inspection:** Loaded `train.csv` using `pandas`. Performed initial checks (shape, dtypes, nulls, basic stats).
2.  **Exploratory Data Analysis (EDA):**
    * Analyzed the target variable `SalePrice`, found it was highly right-skewed, and applied a log transformation (`log1p`) creating `SalePrice_log` for modeling.
    * Calculated and visualized correlations between numerical features and `SalePrice_log` using a heatmap to identify key linear relationships (e.g., `OverallQual`, `GrLivArea_log`, `GarageCars`, `TotalSF`).
    * Visualized relationships between key categorical features (e.g., `OverallQual`, `Neighborhood`, `GarageCars`) and `SalePrice_log` using boxplots.
3.  **Data Cleaning & Preprocessing:**
    * Dropped the `Id` column.
    * Handled missing values based on `data_description.txt`:
        * Filled categorical NaNs meaning 'None' (e.g., `Alley`, `BsmtQual`, `PoolQC`, `Fence`, `FireplaceQu`, `GarageType`, `MasVnrType`) with the string 'None'.
        * Filled numerical NaNs meaning 0 (e.g., `GarageYrBlt`, `MasVnrArea`) with 0.
        * Imputed `LotFrontage` NaNs using the median value of the corresponding `Neighborhood`.
        * Imputed the single `Electrical` NaN with the mode.
    * Checked that all missing values were handled.
4.  **Feature Engineering:**
    * Created new features: `TotalSF`, `HouseAge`, `IsRemodeled`, `YearsSinceRemod`.
    * Log-transformed the skewed `GrLivArea` feature.
5.  **Encoding Categorical Features:**
    * Converted `MSSubClass` (numerical codes representing categories) to string type.
    * Applied One-Hot Encoding (`pd.get_dummies`) to all remaining 'object' type columns. (Note: Treating ordinal features like quality ratings with `OrdinalEncoder` based on `data_description.txt` could be a further improvement).
6.  **Data Splitting:** Separated features (X) and the log-transformed target (y = `SalePrice_log`). Split the data into training (80%) and testing (20%) sets using `train_test_split`.
7.  **Scaling Numerical Features:** Applied `StandardScaler` to all numerical features in X, fitting only on the training data and transforming both training and test sets.
8.  **Modeling:** Trained five different regression models on the preprocessed training data:
    * Linear Regression
    * Ridge Regression
    * Lasso Regression (with a small alpha)
    * Random Forest Regressor
    * Gradient Boosting Regressor
9.  **Evaluation:** Evaluated all models on the test set using:
    * Root Mean Squared Error (RMSE) on the log scale (primary metric).
    * Mean Absolute Error (MAE) on the log scale.
    * R-squared (R²) score.
    * RMSE and MAE on the original dollar scale (after inverse transforming predictions and true values using `np.expm1`) for interpretability.
    * Compared model performance in a summary table.

## Results & Key Findings

* The target variable `SalePrice` was significantly right-skewed and was log-transformed (`SalePrice_log`) for modeling, resulting in a more normal distribution.
* EDA revealed strong positive correlations between `SalePrice_log` and features like `OverallQual`, `GrLivArea_log`, `GarageCars`, `GarageArea`, `TotalSF`, and `1stFlrSF`.
* Categorical features like `OverallQual`, `Neighborhood`, and `GarageCars` showed clear relationships with `SalePrice_log` in boxplots.
* Preprocessing addressed numerous missing values using strategies appropriate to their meaning (e.g., NaN often meant 'None'). One-Hot Encoding significantly increased the number of features.
* **Model Performance Comparison:**
    * **Ridge Regression** emerged as the best-performing model based on the primary metric, **RMSE on the log scale (RMSE_log ≈ 0.1366)**, and also had the highest **R² score (≈ 0.900)**.
    * Gradient Boosting and Random Forest also performed very well, with slightly higher RMSE_log values.
    * Lasso Regression performed poorly with the default settings, likely needing more tuning or indicating less suitability for this specific feature set after OHE.
    * The best model (Ridge) had a **Mean Absolute Error on the original dollar scale of approximately $16,236**, providing an interpretable measure of average prediction error.

## Visualizations

The analysis notebook includes various visualizations:
* Distribution plots (histogram, boxplot) for `SalePrice` and `SalePrice_log`.
* Correlation heatmap for top numerical features vs. `SalePrice_log`.
* Boxplots showing `SalePrice_log` distribution across key categorical features.
* (Potential Future Visualizations: Feature importance plots for tree models, residual plots for model diagnostics).

*(Note: Specific plots are viewable by running the notebook.)*

## Technologies Used

* **Language:** Python (3.x)
* **Core Libraries:**
    * Pandas: Data manipulation and analysis.
    * NumPy: Numerical operations.
    * Matplotlib & Seaborn: Data visualization.
    * Scikit-learn: Preprocessing (StandardScaler, OneHotEncoder), Modeling (LinearRegression, Ridge, Lasso, RandomForestRegressor, GradientBoostingRegressor), Metrics (mean_squared_error, r2_score, mean_absolute_error), `train_test_split`.
    * Re: Regular Expressions (for column renaming).
* **Environment:** Google Colab / Jupyter Notebook

## Installation & Setup

1.  Clone the repository (or download the files).
2.  Ensure you have Python 3 installed.
3.  It is recommended to use a virtual environment:
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows use `venv\Scripts\activate`
    pip install -r requirements.txt
    ```
    *(Note: A `requirements.txt` file should be included in the project folder).*

## Usage

1.  Ensure the required libraries are installed (see Setup).
2.  Open the main notebook (e.g., `house_price_regression.ipynb` - *adjust name if needed*) in Google Colab or a local Jupyter environment.
3.  **Upload the `train.csv` file** using the "Files" panel on the left if using Colab, or place it in the correct directory if running locally.
4.  Run the notebook cells sequentially from top to bottom.
5.  The output will display data inspection details, cleaning steps, EDA plots, model training confirmation, evaluation metrics, and conclusions.
