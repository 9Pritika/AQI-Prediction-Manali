# AQI Prediction and Analysis – Manali, Chennai

## Project Overview

This project focuses on analysing and predicting the Air Quality Index (AQI) using historical hourly air quality data collected from the Manali CPCB monitoring station in Chennai, India.

The project involves data preprocessing, exploratory data analysis, feature engineering and the implementation of machine learning regression models to predict AQI values.

## Dataset

- **Source:** OpenCity – Chennai Hourly Air Quality Reports (2017–2023)
- **Monitoring Station:** Manali CPCB, Chennai
- **Time Period:** July 2017 – December 2023
- **Data Frequency:** Hourly
- **Target Variable:** AQI

The dataset contains hourly AQI readings, including missing observations. The original CSV is included in this repository as `manali.csv`.

## Project Workflow

### 1. Data Preprocessing

- Parsed the original dataset into a structured Pandas DataFrame.
- Converted date information into datetime format.
- Examined missing values and duplicate records.
- Analysed outliers using the Interquartile Range (IQR) method.
- Removed records with missing AQI values for model training.
- Retained outliers because extreme AQI values may represent genuine pollution events.

### 2. Exploratory Data Analysis (EDA)

Visualisations were created using Matplotlib to understand AQI patterns:

- Distribution of AQI readings using histograms.
- AQI outlier analysis using boxplots.
- Missing AQI readings by year.
- Monthly average AQI trends.
- Average AQI by hour of the day.
- Average AQI by month.

### 3. Feature Engineering

The following features were created:

- Hour, Day, Month and Year.
- Day of the week.
- AQI from the previous hour (Lag 1).
- AQI from the previous 24 hours (Lag 24).
- Rolling average AQI of the previous 24 hours.

These features help the models capture temporal patterns and recent AQI behaviour.

### 4. Machine Learning Models

The following regression models were implemented:

1. Dummy Regressor (Baseline)
2. Multiple Linear Regression
3. Random Forest Regressor

A chronological train-test split was used to preserve the time order of observations and avoid randomly mixing past and future data.

### 5. Model Validation and Hyperparameter Tuning

- Time Series Cross-Validation using `TimeSeriesSplit`.
- Hyperparameter tuning of Random Forest using `GridSearchCV`.
- Evaluation of the tuned Random Forest model on the test dataset.

### 6. Model Evaluation

The models were evaluated using:

- Mean Absolute Error (MAE)
- Mean Squared Error (MSE)
- Root Mean Squared Error (RMSE)
- R² Score

Error analysis was also performed to understand prediction errors and identify cases where the model struggled.

## Results

The following results were obtained on the chronological test dataset:

| Model | MAE | RMSE | R² Score |
|---|---:|---:|---:|
| Baseline | 30.29 | 45.89 | -0.028 |
| Multiple Linear Regression | 16.56 | 30.17 | 0.556 |
| Random Forest | 18.21 | 32.86 | 0.473 |
| Tuned Random Forest | 16.94 | 32.13 | 0.496 |

Multiple Linear Regression achieved the best test performance among the evaluated models, with an MAE of approximately 16.56 and an R² score of 0.556.

### Prediction Error Analysis

The Multiple Linear Regression model achieved the following results on the test dataset:

- **77.61%** of predictions were within 20 AQI points of the actual values.
- **51.94%** of predictions were within 10 AQI points of the actual values.
- **Mean Absolute Error (MAE):** 16.56 AQI points.
- **Median Absolute Error:** 9.48 AQI points.

Although the model performed reasonably well for many observations, larger prediction errors occurred during unusual or extreme AQI conditions.

## Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Scikit-learn
- Google Colab
- Jupyter Notebook

## How to Run

### Using Google Colab

1. Open `Air_Quality_Analysis.ipynb` in Google Colab.
2. Run the notebook cells in order.
3. Upload `manali.csv` when prompted.
4. Execute all cells to reproduce the analysis and model evaluation.

### Using Local Jupyter Notebook

1. Clone or download this repository.
2. Install the required dependencies using:

   `pip install -r requirements.txt`

3. Keep `Air_Quality_Analysis.ipynb` and `manali.csv` in the same directory.
4. Open the notebook in Jupyter Notebook or JupyterLab.
5. Run all cells in order.

## Limitations

- The dataset contains missing AQI observations.
- Model performance depends on historical patterns in the available dataset.
- Extreme AQI values can result in larger prediction errors.
- The evaluation measures performance on historical test data; it does not establish forecasting accuracy for future dates.
- The dataset ends in 2023 and does not contain recent real-time AQI observations.

## Future Improvements

- Incorporate additional air quality parameters such as PM2.5, PM10, NO₂ and CO.
- Explore additional time-series forecasting approaches.
- Evaluate models using more recent AQI observations.

---

**Project:** AQI Prediction and Analysis – Manali, Chennai  
**Data Source:** CPCB via OpenCity

