# Boston Crime Data - Exploratory Data Analysis (EDA)

## Project Overview

This project performs an in-depth Exploratory Data Analysis (EDA) on the Boston Crime dataset. The primary goal is to clean, explore, and visualize the data to uncover patterns, trends, and insights related to criminal incidents in Boston. This includes analyzing crime types, occurrence times, locations, and other relevant factors. The focus is on understanding the data's characteristics and communicating findings through visualizations.

## Motivation

Analyzing crime data is crucial for various stakeholders:
* **Public Safety:** Understanding crime patterns helps law enforcement allocate resources more effectively and develop targeted prevention strategies.
* **Urban Planning & Policy:** Identifying crime hotspots and trends can inform urban planning decisions and public policy initiatives.
* **Community Awareness:** Providing insights into local crime statistics can raise community awareness and engagement.
* **Research:** Serving as a basis for further academic or sociological research into the causes and effects of crime.

This EDA aims to provide a comprehensive overview of the dataset's structure, identify potential data quality issues, and reveal initial patterns related to crime in Boston.

## Data Source

* **Dataset:** Boston Crime Dataset (containing incident reports)
* **Source:** Kaggle - Analyze Boston (`AnalyzeBoston/crimes-in-boston`). Link: [https://www.kaggle.com/datasets/AnalyzeBoston/crimes-in-boston](https://www.kaggle.com/datasets/AnalyzeBoston/crimes-in-boston)
* **Files Used:**
    * `crime.csv`: Main file containing crime incident reports.
    * `offense_codes.csv`: File mapping offense codes to descriptive names.
* **Loading Method:** The accompanying notebook (`boston_crime_eda.ipynb` - *adjust name if different*) uses manual file upload via the Google Colab interface for both CSV files.

## Methodology

The project follows these key EDA steps:

1.  **Data Loading & Initial Inspection:** Loading both `crime.csv` and `offense_codes.csv` using `pandas`, handling potential encoding issues (`latin-1`). Performing initial checks on data shapes, column names, data types, and null values for both datasets.
2.  **Data Cleaning & Preprocessing:**
    * Renaming columns to a consistent `snake_case` format.
    * Converting the `occurred_on_date` column to `datetime` objects, handling and dropping invalid date entries.
    * Cleaning `lat` and `long` columns by replacing placeholder values (`-1.0`) with `NaN`.
    * Handling duplicates in `offense_codes.csv` before merging.
    * **Merging:** Joining the crime data (`df_crime`) with offense code descriptions (`df_codes`) based on the `offense_code`.
    * **Handling Null Values:** Addressing missing data in key columns (`shooting`, `street`, `district`, `ucr_part`) using appropriate strategies (e.g., filling with 0, 'Unknown', mode, or dropping rows). Nulls in `lat`/`long` were kept for potential later analysis. Nulls in `offense_name` resulting from the merge were filled.
    * **Feature Engineering:** Creating new time-based features (e.g., `month`, `day_of_week`, `hour`, `year`) from the `occurred_on_date` column.
3.  **Univariate Analysis:** Analyzing the distribution of individual variables, including:
    * Top N offense types (using descriptive names from the merge).
    * Incident distribution across districts.
    * Incident distribution by day of the week and hour of the day.
    * Distribution of shooting incidents.
    * Distribution of latitude/longitude (for valid coordinates).
4.  **Bivariate & Multivariate Analysis (Planned):** Exploring relationships between variables (e.g., crime type vs. time, crime type vs. district).
5.  **Temporal Analysis (Planned):** Investigating trends, seasonality, and patterns over time (years, months, days, hours).
6.  **Geospatial Analysis (Planned):** Visualizing crime data geographically using latitude and longitude (e.g., heatmaps, point maps), if data quality permits after handling nulls.
7.  **Conclusions:** Summarizing key findings and insights from the EDA.

## Key Findings (Initial)

* The dataset contains over 300,000 crime incident reports.
* Significant missing data was observed for `shooting` incidents (over 99% missing, likely indicating non-shooting events), location coordinates (`lat`, `long`, ~6-7% missing after cleaning invalid values), and `street` names (~3%). Missing values in `district` and `ucr_part` were less frequent.
* The `offense_codes.csv` file contained duplicate codes, which were handled before merging to avoid inflating incident counts.
* Initial univariate analysis revealed common offense types (e.g., [Mention Top 1-2 from your plots if available, otherwise keep general]), distinct patterns in crime occurrences based on the district, day of the week (e.g., peaks on certain days), and hour of the day (e.g., peaks during specific time windows).

*(Note: More detailed findings will emerge as bivariate, temporal, and geospatial analyses are completed.)*

## Visualizations

The analysis currently includes univariate visualizations generated within the notebook:

* Bar charts showing the distribution of top offense types, incidents per district, per day of the week, and per hour.
* Count plot for shooting incidents.
* Histograms for latitude and longitude distributions.

Planned visualizations include time series plots, heatmaps (temporal or geospatial), geospatial maps (using libraries like Folium or Geopandas), and plots exploring relationships between variables.

*(Note: Specific plots are viewable by running the notebook.)*

## Technologies Used

* **Language:** Python (3.x)
* **Core Libraries:**
    * Pandas: Data manipulation and analysis.
    * NumPy: Numerical operations.
    * Matplotlib & Seaborn: Data visualization.
    * Re (Regular Expressions): For column renaming.
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
2.  Open the main notebook (e.g., `boston_crime_eda.ipynb` - *adjust name if needed*) in Google Colab or a local Jupyter environment.
3.  **Upload both `crime.csv` and `offense_codes.csv`** using the "Files" panel on the left if using Colab, or place them in the correct directory if running locally.
4.  Run the notebook cells sequentially.
5.  The output will display data inspection details, cleaning steps, and exploratory visualizations.

---
