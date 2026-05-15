# Energy Market Price Prediction

This project builds an energy market dataset and predicts Market Clearing Price (MCP) using market, grid generation, renewable, and weather-derived features.

## Contents

- `energy_dataset.ipynb` - data preparation, feature engineering, EDA, model training, model comparison, prediction plots, residual analysis, and feature importance.

## Notes

- The notebook expects the source Excel files to be available in the paths used inside the data-loading cells.
- Add your own OpenWeather API key in the forecast weather experiment cell before running that optional section.
- The final modeling section uses a time-based train/test split and compares several regression models.
