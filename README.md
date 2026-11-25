# COVID-19 Forecasting and Analysis with Prophet

A Python-based time-series analysis project that explores global and
India-specific COVID-19 trends, visualizes confirmed cases, deaths,
recoveries, and active cases, and uses Facebook Prophet to forecast
future case trends.

## Project Overview

The notebook analyzes COVID-19 data over time and addresses the
following problem:

> Visualize the impact of COVID-19, analyze infection and recovery
> trends, and predict future case counts based on historical trends.

The notebook compares some limitations of traditional ARIMA/SARIMA
approaches and demonstrates Prophet as an accessible forecasting
alternative.

## Features

-   Load and inspect the COVID-19 dataset with pandas.
-   Convert the `Date` column to datetime format.
-   Identify the date range and number of countries in the dataset.
-   Aggregate confirmed cases, deaths, recoveries, and active cases
    globally by date.
-   Inspect the most recent country-level observations.
-   Find countries with the highest confirmed case counts and deaths.
-   Plot global confirmed-case trends and daily new confirmed cases.
-   Fit Prophet models to global confirmed cases and daily new cases.
-   Calculate recovery, mortality, and infection growth rates.
-   Create interactive Plotly line charts for global trends and rates.
-   Create an interactive choropleth map showing confirmed cases by
    country.
-   Visualize Prophet forecasts and forecast components.
-   Extract a seven-day forecast and build an India-specific trend
    analysis and forecast.

## Technologies Used

-   Python
-   Jupyter Notebook
-   pandas
-   NumPy
-   Matplotlib
-   Seaborn
-   Facebook Prophet (`prophet`)
-   Plotly
-   statsmodels is not required by the notebook's main forecasting
    workflow.

## Project Files

The notebook expects a dataset named:

``` text
Covid_19_Clean_Complete (2).csv
```

Place the CSV file in the same directory as the notebook, or update the
path in the notebook to match your file location.

The main notebook is:

``` text
covid_19_project.ipynb
```

## Requirements and Installation

Use Python in an environment that supports Jupyter Notebook.

Install the packages used in the notebook:

``` bash
pip install pandas numpy matplotlib seaborn prophet plotly jupyter
```

If Prophet installation fails, check the official Prophet installation
instructions for your operating system and Python version.

## How to Run

1.  Download or clone this project and make sure the CSV dataset is
    available.

2.  Open a terminal in the project folder.

3.  Install the required packages.

4.  Launch Jupyter Notebook:

    ``` bash
    jupyter notebook
    ```

5.  Open `covid_19_project.ipynb`.

6.  Run the notebook cells in order.

The notebook also includes a `pip install prophet` cell for notebook
environments where Prophet is not already installed.

## Analysis Workflow

### 1. Data loading and inspection

The notebook reads the CSV with pandas, inspects its shape and data
types, previews rows, converts `Date` to datetime, and renames
`Province/State` to `State` and `Country/Region` to `Country`.

### 2. Global aggregation

Records are grouped by date and the following measures are summed:

-   `Confirmed`
-   `Deaths`
-   `Recovered`
-   `Active`

### 3. Country comparisons

The notebook selects the most recent date in the dataset, aggregates
totals by country, and identifies countries with the most confirmed
cases and deaths. It also inspects India's latest available record.

### 4. Trend visualizations

Line charts are used to display global confirmed cases and daily new
confirmed cases. Plotly adds interactive charts for confirmed,
recovered, active, and death counts, plus recovery and mortality rates.
A choropleth map compares confirmed cases by country.

### 5. Rate calculations

The notebook calculates:

-   **Recovery Rate (%)** = Recovered / Confirmed × 100
-   **Mortality Rate (%)** = Deaths / Confirmed × 100
-   **Infection Growth Rate (%)** = New Cases / Confirmed × 100

These are the formulas implemented in the notebook. The infection growth
rate here is specifically calculated using new cases divided by
cumulative confirmed cases; it is not the percentage change in new cases
from the previous day.

### 6. Prophet forecasting

The notebook prepares Prophet input using the required column names:

-   `ds`: date
-   `y`: target value to forecast

It fits Prophet models for global confirmed cases and daily new cases,
creates future dates, generates predictions, and plots the forecasts. It
also experiments with `seasonality_mode="multiplicative"`.

### 7. Seven-day forecast and India analysis

The notebook extracts seven forecast rows after **2020-07-27** for daily
new cases, showing the predicted value (`yhat`) and lower and upper
bounds (`yhat_lower`, `yhat_upper`).

It also filters the dataset for India, calculates daily new cases and
recovery rate, plots India's trend, and fits a Prophet model to forecast
India's confirmed-case series for seven future days.

## Understanding Prophet Forecast Output

The forecast includes:

-   `yhat`: predicted value.
-   `yhat_lower`: lower bound of the model's uncertainty interval.
-   `yhat_upper`: upper bound of the model's uncertainty interval.

These are model estimates, not guaranteed outcomes. Forecast quality
depends on data quality, the date range, the model configuration, and
changes in real-world conditions.

## Important Notes and Limitations

-   This is a historical COVID-19 analysis notebook. Its seven-day
    extraction is anchored to **2020-07-27**, and the country map title
    also references that date. It should not be interpreted as a current
    COVID-19 forecast.
-   The CSV dataset is required but is not included by this README.
    Obtain the appropriate dataset and verify its source and usage terms
    before running the notebook.
-   The notebook uses cumulative counts for some plots and forecasts
    daily new cases in another section. These are different target
    variables and should not be confused.
-   The notebook creates a future dataframe of 31 periods in one section
    and extracts seven days in another. The India-specific model uses
    seven future periods.
-   The notebook contains a compatibility workaround that temporarily
    changes pandas Series/DataFrame boolean behavior around interactive
    Prophet plotting. Such monkey-patching can be fragile across library
    versions; if plotting fails, check the installed Prophet, pandas,
    and Plotly versions and prefer a compatible environment.
-   The notebook's calculated rates may be undefined if confirmed cases
    are zero. Check for division-by-zero and missing values when
    adapting the analysis.
-   For a stronger forecasting evaluation, reserve the latest
    observations as a chronological test set and compare predictions
    with actual values using appropriate error metrics. Avoid treating
    the lowest training error as proof of future accuracy.

## Possible Improvements

-   Add explicit data-source attribution and dataset licensing
    information.
-   Validate missing values, duplicate records, and unexpected negative
    daily differences.
-   Ensure observations are sorted by date before calculating
    differences.
-   Add forecast evaluation with MAE or RMSE on a held-out time period.
-   Compare additive and multiplicative seasonality using a consistent
    evaluation method.
-   Save forecast tables and charts as output files.
-   Add a requirements file to make the environment easier to reproduce.

## Learning Outcomes

By working through this notebook, you can practice:

-   Time-series data cleaning and aggregation.
-   Exploratory data analysis and visualization.
-   Creating daily case counts from cumulative counts.
-   Calculating simple epidemiological rates.
-   Using Prophet for time-series forecasting.
-   Building interactive Plotly charts and a choropleth map.
-   Interpreting forecast values and uncertainty intervals.

------------------------------------------------------------------------

**Project type:** Data analysis and time-series forecasting\
**Primary notebook:** `covid_19_project.ipynb`
