# Bank Customer Churn Prediction Project

## Overview

This project focuses on **predicting customer churn** for a banking institution using machine learning. The goal is to identify customers who are likely to stop using the bank's services based on their demographics and past behavior. By proactively identifying these at-risk customers, the bank can implement targeted retention strategies, which are often more cost-effective than acquiring new customers.

This project demonstrates an end-to-end data science workflow, including data exploration, preprocessing, handling class imbalance, model training, evaluation, and interpretation.

## Motivation / Problem Statement

Customer churn, or attrition, is a critical metric for subscription-based businesses and service providers like banks. High churn rates can significantly impact revenue and growth. Understanding the factors that drive churn and building accurate predictive models allows businesses to:
* Implement targeted retention campaigns.
* Optimize resource allocation for customer relationship management.
* Improve customer satisfaction by addressing pain points.
* Ultimately, reduce revenue loss associated with departing customers.

## Data Source

* **Dataset:** Bank Customer Churn Prediction
* **Source:** Originally from Kaggle. The specific version used in the notebook is often found at sources like: [https://www.kaggle.com/datasets/shubhammeshram579/bank-customer-churn-prediction](https://www.kaggle.com/datasets/shubhammeshram579/bank-customer-churn-prediction) (Please verify this is the exact source you used).
* **Loading:** The accompanying notebook (`bank_churn_analysis.ipynb` - *adjust name if different*) uses manual file upload via the Google Colab interface. The expected filename is `Bank Customer Churn Prediction.csv`.

## Methodology / Approach

The project follows these key steps:

1.  **Data Loading & Initial Exploration:** Loading the dataset and performing initial checks (shape, data types, null values, basic statistics).
2.  **Exploratory Data Analysis (EDA):** Deep dive into the data using visualizations (histograms, box plots, count plots, correlation matrix) to understand feature distributions, relationships, and how features correlate with the target variable (`churn`).
3.  **Data Preprocessing:**
    * Dropping irrelevant columns (`customer_id`).
    * Handling missing values (if any - none were found in this dataset).
    * Encoding categorical features (`country`, `gender`) using One-Hot Encoding.
    * Scaling numerical features using StandardScaler.
    * Creating a preprocessing pipeline using Scikit-learn's `ColumnTransformer`.
4.  **Handling Class Imbalance:** Addressing the imbalance in the target variable (`churn` ~20%) using SMOTE (Synthetic Minority Over-sampling Technique) via the `imblearn` library within the modeling pipeline (if `imblearn` is installed) or using `class_weight='balanced'` in the classifiers.
5.  **Model Training:** Training and comparing two common classification models:
    * Logistic Regression
    * Random Forest Classifier
6.  **Model Evaluation:** Evaluating model performance on the test set using various metrics suitable for imbalanced classification:
    * Accuracy
    * Confusion Matrix
    * Classification Report (Precision, Recall, F1-Score - especially for the 'Churn' class)
    * ROC Curve and AUC (Area Under the Curve)
    * Precision-Recall Curve and PR AUC
7.  **Model Interpretation:** Analyzing feature importances from the best-performing model (Random Forest in this case) to understand the key drivers of churn.

## Results & Key Findings

* The **Random Forest** model demonstrated the best overall performance based on the evaluation metrics.
* **Key Metrics (Random Forest):**
    * AUC: ~0.8665
    * F1-Score (Churn Class): ~0.6290
    * Accuracy: ~0.8344
* **Top 3 Most Important Features** identified by the Random Forest model were:
    1.  `age`
    2.  `products_number` (Number of products the customer holds)
    3.  `balance` (Customer's account balance)
* These findings suggest that customer age, their engagement with the bank via the number of products, and their account balance are significant factors influencing the likelihood of churn.

## Visualizations

The analysis includes several visualizations generated within the notebook to understand the data and model performance:

* Distribution plots (histograms, box plots) for numerical features, segmented by churn status.
* Count plots showing churn distribution across categorical features (e.g., country, gender).
* Correlation heatmap for numerical features.
* Confusion matrices for trained models.
* ROC curves and Precision-Recall curves for visual performance assessment.
* Bar chart displaying the top feature importances from the Random Forest model.

*(Note: Specific plots are viewable by running the notebook.)*

## Technologies Used

* **Language:** Python (3.x)
* **Core Libraries:**
    * Pandas: Data manipulation and analysis.
    * NumPy: Numerical operations.
    * Scikit-learn: Preprocessing, modeling, evaluation, pipelines.
    * Matplotlib & Seaborn: Data visualization.
    * Imbalanced-learn (Optional, if installed): SMOTE for handling class imbalance.
* **Environment:** Google Colab / Jupyter Notebook

## Installation & Setup

1.  Clone the repository (or download the files).
2.  Ensure you have Python 3 installed.
3.  Install the required libraries. It is recommended to use a virtual environment:
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows use `venv\Scripts\activate`
    pip install -r requirements.txt
    ```
    *(Note: A `requirements.txt` file should be included in the project folder)*

## Usage / How to Run

1.  Ensure the required libraries are installed (see Setup).
2.  Open the main notebook (e.g., `bank_churn_analysis.ipynb` - *adjust name if needed*) in Google Colab or a local Jupyter environment.
3.  If running in Colab, upload the `Bank Customer Churn Prediction.csv` dataset using the "Files" panel when prompted by the initial data loading cell (or ensure it's present in the `/content/` directory). If running locally, place the CSV in the same directory as the notebook or update the file path accordingly.
4.  Run the notebook cells sequentially from top to bottom.
5.  The results, including EDA plots, model evaluations, and feature importances, will be displayed within the notebook.

---
