# California Housing Prices Project: Data Analysis and Interactive Dashboard

## Table of Contents
1.  [Project Overview](#project-overview)
2.  [Dataset](#dataset)
3.  [Analysis Steps](#analysis-steps)
    *   [Data Loading & Initial Exploration](#data-loading--initial-exploration)
    *   [Data Preprocessing & Feature Engineering](#data-preprocessing--feature-engineering)
    *   [Data Cleaning](#data-cleaning)
    *   [Descriptive Statistics](#descriptive-statistics)
    *   [Advanced Data Exploration & Group Analysis](#advanced-data-exploration--group-analysis)
    *   [Visualizations](#visualizations)
    *   [Hard Analysis Questions](#hard-analysis-questions)
    *   [Final Report](#final-report)
4.  [Streamlit Dashboard](#streamlit-dashboard)
5.  [Key Findings & Insights](#key-findings--insights)
6.  [Limitations](#limitations)
7.  [Future Work](#future-work)

## Project Overview
This project involves a comprehensive data analysis of the California Housing dataset to understand the factors influencing median house values. It covers data loading, preprocessing, cleaning, exploratory data analysis (EDA) with advanced statistical techniques, and visualization. The project culminates in a final report summarizing findings and an interactive Streamlit dashboard for dynamic data exploration.

## Dataset
The dataset used is the California Housing dataset, obtained from the StatLib repository via `sklearn.datasets.fetch_california_housing`. It contains 8 numerical predictive attributes and a target variable (Median House Value) for California districts based on the 1990 U.S. Census.

**Attributes:**
*   `MedInc`: median income in block group
*   `HouseAge`: median house age in block group
*   `AveRooms`: average number of rooms per household
*   `AveBedrms`: average number of bedrooms per household
*   `Population`: block group population
*   `AveOccup`: average number of household members
*   `Latitude`: block group latitude
*   `Longitude`: block group longitude
*   `MedHouseVal`: median house value for California districts, expressed in hundreds of thousands of dollars ($100,000).

## Analysis Steps

### Data Loading & Initial Exploration
*   Loaded the dataset into a pandas DataFrame.
*   Reported data shape, feature names, and a detailed description of the target variable.
*   Formulated initial hypotheses regarding the association of median income, house age, and geographical location with median house value.

### Data Preprocessing & Feature Engineering
*   Checked data types (all confirmed numerical).
*   Scaled all features using `StandardScaler` to ensure uniformity.
*   Created new features to capture more complex relationships:
    *   `RoomsPerHousehold`
    *   `BedroomsPerRoom`
    *   `PopulationDensity`
    *   `IncomePerPerson`
*   Scaled these newly engineered features and integrated them into the main scaled DataFrame.

### Data Cleaning
*   **Missing Values:** Artificially introduced 5% missing values in the `HouseAge` column and demonstrated mean and median imputation. Median imputation was chosen for robustness against outliers.
*   **Outlier Detection & Handling:** Artificially introduced 10 outliers in `MedInc` and detected them using both Z-score and IQR methods. Outliers were capped using the IQR bounds, explaining the decision to cap rather than remove to retain data integrity.

### Descriptive Statistics
*   Computed mean, median, variance, skewness, and kurtosis for all features.
*   Identified `AveOccup` as the most skewed feature and `HouseAge` as the most approximately normal.
*   Ranked features by variance, revealing `Population`, `PopulationDensity`, and `HouseAge` as the most varying features.
*   Identified `IncomePerPerson` as the feature most strongly correlated with `MedHouseVal` (0.7456), followed by `MedInc` (0.6867).

### Advanced Data Exploration & Group Analysis
*   **Binning & Grouping:** `HouseAge` was binned into 'Young', 'Middle', and 'Old' groups, and mean/variance of `MedHouseVal` were computed for each.
*   **Income Segmentation:** `MedInc` was segmented into four quartiles (Q1-Q4), and average `MedHouseVal`, `AveRooms`, and `Population` were compared across these quartiles.
*   **Geographical Analysis:** Divided the dataset into 'North' and 'South' California based on median latitude and compared median house values and average incomes. Visualized this comparison using side-by-side bar charts, noting that the South generally has higher median house values and average incomes.
*   **Feature Ratios & Insights:** Analyzed the distributions of `RoomsPerHousehold` and `BedroomsPerRoom` through histograms and boxplots, providing interpretations of extreme values.
*   **Cross-tabulation:** Created a cross-tabulation between `HouseAge` groups and `IncomeQuartile` with average `MedHouseVal`, identifying the highest ('Old', 'Q4') and lowest ('Young', 'Q1') value combinations.

### Visualizations
*   **Univariate Plots:** Histograms for `MedInc`, `HouseAge`, `AveRooms`, and `MedHouseVal`, revealing distribution characteristics (skewness, top-coding effects).
*   **Bivariate Plots:**
    *   Scatter plot of `MedInc` vs. `MedHouseVal` with a regression line, showing a strong positive correlation.
    *   Scatter plot of `AveRooms` vs. `MedHouseVal`, indicating a weaker, noisier positive relationship.
    *   Violin plot for `HouseAge` across binned `MedHouseVal` categories (Low/Medium/High).
    *   Grouped bar chart for `PopulationDensity` bins vs. average house value.
*   **Multivariate & Advanced Plots:**
    *   Correlation heatmap of all features, highlighting `IncomePerPerson` and `MedInc` as the strongest correlations with `MedHouseVal`.
    *   Pairplot for selected key features (`MedInc`, `HouseAge`, `AveRooms`, `MedHouseVal`) to visualize inter-feature relationships.
    *   3D scatter plot of (`Longitude`, `Latitude`, `MedHouseVal`) to discuss geographic trends, identifying high-value clusters around San Francisco Bay Area and coastal Southern California.
    *   Combined subplot figure for an executive technical dashboard, summarizing key distributions, economic drivers, and correlations.

### Hard Analysis Questions
*   **Top Features for `MedHouseVal`:** `IncomePerPerson`, `MedInc`, and `BedroomsPerRoom` were identified as the top 3 features based on correlation and variance.
*   **Within-Group Variance (HouseAge):** Computed within-group variance of `MedHouseVal` for `HouseAge` quartiles, finding the 'Q1' (Young) group to be the most consistent.
*   **Between-Group Variance (Income Quartiles):** Computed between-group variance of `MedHouseVal` across income quartiles, showing significant differences, particularly between 'Q1' and 'Q4'.
*   **Mahalanobis Distance:** Calculated Mahalanobis distance between high-income (Q4) and low-income (Q1) neighborhoods using standardized features, interpreting the result as a measure of multivariate separation.

### Final Report
*   **Hypotheses Confirmation:** Verified initial hypotheses regarding median income, house age, and geographical influence on house values, providing nuanced explanations for each.
*   **Key Insights:** Highlighted findings such as `IncomePerPerson` being a better predictor than `MedInc`, house age amplifying price uncertainty, and the distinction between variance and predictive power.

## Streamlit Dashboard
An interactive Streamlit dashboard (`app.py`) was created to visualize the geographic distribution of housing prices, income vs. house value relationships, and a feature correlation heatmap. Users can filter data by Median Income Range and House Age Category.

**How to run the dashboard:**
1.  Ensure you have `streamlit` installed (`pip install streamlit`).
2.  Run the `%%writefile app.py` cell to create the `app.py` file.
3.  Execute the `!streamlit run app.py` command (or the provided `pyngrok` setup in the notebook) to launch the dashboard.

## Key Findings & Insights
1.  **Per-capita income predicts price better than household income:** `IncomePerPerson` (r = 0.7456) correlates more strongly with `MedHouseVal` than raw `MedInc` (r = 0.6867).
2.  **House age amplifies uncertainty:** Youngest homes (Q1) are most price-consistent, while oldest homes (Q4) show the most price variability.
3.  **High variance does not imply predictive power:** Features like `Population` can have high variance but low correlation with `MedHouseVal`.
4.  **Geographic clusters are key:** High-value areas are concentrated around the San Francisco Bay Area and coastal Southern California, indicating coastal proximity as a significant driver.

## Limitations
*   **Outdated Data:** 1990 U.S. Census data may not reflect current market dynamics.
*   **Top-coding:** `HouseAge` and `MedHouseVal` are capped, limiting the analysis of extreme values.
*   **Missing Socioeconomic Features:** Lack of data on crime rates, school quality, etc., which are known housing price drivers.
*   **Aggregated Data:** Block-group averages can mask within-block heterogeneity.

## Future Work
*   Incorporate external datasets (crime, schools, employment).
*   Engineer a "distance to coast".
*   Refresh the data.
*   Create predictive model.
