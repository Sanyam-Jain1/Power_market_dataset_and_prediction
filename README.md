# Power Market Dataset and Prediction

This repository contains a complete notebook workflow for building a power market dataset and predicting Market Clearing Price (MCP). The project combines market bidding data, grid generation data, renewable generation indicators, and weather-based features to explore what drives electricity prices and to train regression models for MCP prediction.

## Project Overview

Electricity market prices are influenced by demand, supply, renewable generation, weather, and recent price behavior. This project creates a structured dataset from collected power market data, performs exploratory data analysis, engineers useful features, and compares multiple machine learning models for MCP prediction.

The notebook is designed as an end-to-end analysis pipeline:

1. Load and clean market snapshot data.
2. Create time-based and lag-based features.
3. Fetch and aggregate city-level weather information.
4. Merge grid demand and generation data.
5. Build a final modeling dataset.
6. Perform EDA with charts and correlation analysis.
7. Train and compare multiple prediction models.
8. Plot actual vs predicted MCP and model errors.
9. Export prediction and model-comparison outputs.

## Repository Contents

| File | Description |
| --- | --- |
| `energy_dataset.ipynb` | Main Jupyter notebook containing data cleaning, feature engineering, EDA, model training, evaluation, prediction plots, residual analysis, and feature importance. |
| `power_dataset_created.xlsx` | Created power market dataset used for analysis and model experimentation. |
| `README.md` | Project documentation. |

## Dataset

The created dataset includes market, grid, renewable, weather, and time-based variables.

Key target:

- `mcp` - Market Clearing Price, the prediction target.

Important feature groups:

- Market features: `purchase_bid`, `sell_bid`, `imbalance`, `mcv`, `final_volume`
- Time features: `hour`, `day_of_week`, `is_weekend`
- Lag features: `price_t-1`, `price_t-4`
- Grid features: `grid_demand`, `wind_gen`, `solar_gen`, `total_gen`
- Derived power features: `net_demand`, `renewable_ratio`
- Weather features: `avg_temp`, `max_temp`, `avg_humidity`, `avg_wind`, `avg_sun`, `max_sun`

## Exploratory Data Analysis

The notebook includes visual analysis to understand MCP behavior and relationships between variables:

- MCP trend over time
- MCP distribution
- MCP by hour of day
- Weekday vs weekend price behavior
- Scatter plots against demand, renewable ratio, temperature, humidity, and wind
- Correlation heatmap
- Correlation ranking against MCP

These plots help identify the strongest market, demand, renewable, and weather signals before modeling.

## Prediction Models

The final section trains and compares several regression models using a time-based train/test split:

- Linear Regression
- Ridge Regression
- Lasso Regression
- ElasticNet
- Random Forest Regressor
- Extra Trees Regressor
- Gradient Boosting Regressor
- Hist Gradient Boosting Regressor
- XGBoost Regressor, if `xgboost` is installed

Model performance is compared using:

- MAE - Mean Absolute Error
- RMSE - Root Mean Squared Error
- R2 Score
- MAPE - Mean Absolute Percentage Error

The best model is selected based on RMSE and used for final prediction visualizations.

## Output Visualizations

The modeling section generates:

- Model comparison bar chart
- Actual vs predicted MCP over the test period
- Zoomed actual vs predicted plot for the first test points
- Actual vs predicted scatter plot
- Prediction error distribution
- Prediction error over time
- Top feature-importance chart for supported models

## Generated Output Files

When the final notebook section is run, it saves:

- `mcp_predictions.xlsx` - actual MCP, predicted MCP, and prediction errors for the test period
- `model_comparison.xlsx` - model evaluation metrics

These generated files are not required to understand the repo, but they are useful after running the notebook.

## Setup

Install the common Python libraries used in the notebook:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn openpyxl meteostat requests
```

Optional, for XGBoost:

```bash
pip install xgboost
```

## How to Run

1. Open `energy_dataset.ipynb` in Jupyter Notebook, JupyterLab, Google Colab, or VS Code.
2. Make sure the source Excel files referenced in the loading cells are available.
3. Run the notebook cells in order.
4. Use `power_dataset_created.xlsx` as the prepared dataset if you want to start directly from the collected dataset.
5. Run the final EDA and prediction section to generate charts, model metrics, and prediction outputs.

## API Key Note

The optional forecast weather experiment uses OpenWeather. The notebook contains a placeholder:

```python
API_KEY = "YOUR_OPENWEATHER_API_KEY"
```

Replace it with your own key before running that optional section. Do not commit real API keys to GitHub.

## Methodology Notes

- The prediction workflow uses a time-based split instead of a random split, which is more appropriate for time-dependent market data.
- Missing numeric values are handled with median imputation inside the modeling pipeline.
- Numeric features are scaled before model training.
- The notebook keeps a stable copy of the final prepared dataset as `model_dataset` so later experiment cells do not overwrite the modeling data.

## Project Goal

The goal is to create a clean, explainable, and extensible workflow for power market MCP prediction. The project can be extended with more historical data, richer weather signals, holiday indicators, load forecasts, renewable forecasts, and hyperparameter tuning.
