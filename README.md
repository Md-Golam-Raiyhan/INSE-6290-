# INSE 6290 – Final Project
AI-Based Demand Forecasting and Inventory Optimization for Food Delivery Supply Chains

## Dependencies

Python 3.9+

Install required packages:

```bash
pip install pandas numpy matplotlib scikit-learn scipy streamlit plotly
```

---

## How to Run the Code

Open the main project notebook or run the Python pipeline files from the project folder.

### Option 1: Run the notebook
Open:

```bash
main.ipynb
```

Run all cells from top to bottom.

The notebook:

- Loads the real foodDemand dataset using relative paths
- Selects the top 10 meals by total demand
- Aggregates weekly demand across fulfillment centers
- Performs feature engineering
- Trains baseline and AI-based forecasting models
- Applies inventory optimization using the newsvendor model
- Simulates weekly operations with FEFO perishability logic
- Computes forecasting and supply chain performance metrics
- Generates tables and plots for the final report

### Option 2: Run the Python pipeline
If your project package includes script files such as `run_project.py`, `pipeline.py`, or `app.py`, run:

```bash
python run_project.py
```

To launch the dashboard:

```bash
streamlit run app.py
```

---

## Project Description

This project develops an integrated decision-support system for food delivery supply chains. The system combines:

- demand forecasting
- inventory optimization
- simulation-based evaluation

The project uses the real **foodDemand** dataset and focuses on the top 10 high-demand meals aggregated at weekly level. Two forecasting approaches are compared:

- Baseline Lag-4 model
- Random Forest model

Forecast outputs are then used in a **newsvendor inventory optimization model**. The resulting order quantities are evaluated through simulation using a **First Expire First Out (FEFO)** inventory policy.

---

## Dataset Description

The project uses the following files:

- `train.csv` – historical weekly demand records
- `meal_info.csv` – meal category and cuisine information
- `fulfilment_center_info.csv` – fulfillment center metadata
- `food_Demand_test.csv` – reference test split (if included)

Dataset preparation includes:

- selecting the top 10 meals by total demand
- aggregating demand across all fulfillment centers
- generating lag, rolling-average, price, promotion, and seasonal features
- splitting data into training and testing sets

Generated working datasets may include:

- `top_10_meals_by_total_demand.csv`
- `aggregated_top10_meals_weekly.csv`
- `prepared_dataset_with_features.csv`
- `train_prepared_dataset.csv`
- `test_prepared_dataset.csv`

---

## Forecasting Model Description

### Baseline Model
The baseline model uses a **Lag-4** demand estimate, where demand from four weeks earlier is used as the current forecast.

### AI Model
The AI forecasting model is a **Random Forest Regressor** trained on engineered features such as:

- lag_1
- lag_4
- rolling_4
- rolling_8
- checkout_price
- base_price
- price_ratio
- price_discount
- emailer_for_promotion
- homepage_featured
- week_of_year
- meal_id

### Forecast Evaluation Metrics
The forecasting models are evaluated using:

- MAE
- RMSE

---

## Inventory Optimization

The project uses a **newsvendor-based inventory optimization model** to determine weekly order quantities.

Inputs include:

- forecast mean demand
- forecast uncertainty
- shortage cost
- holding cost

The order quantity is calculated using the forecast and uncertainty terms, with a service-level factor derived from the critical ratio.

---

## Simulation Logic

The simulation evaluates how forecasting and inventory decisions perform over time.

The simulation process includes:

- receiving weekly demand
- using forecast values to compute order quantity
- updating inventory by age bucket
- applying FEFO logic
- tracking expired inventory as waste
- tracking unmet demand as stockout
- computing revenue, cost, and gross profit

Two simulation scenarios are compared:

- Baseline forecasting + inventory policy
- AI-RF forecasting + inventory policy

---

## Performance Metrics

The project evaluates both forecasting and supply chain performance.

### Forecasting metrics
- MAE
- RMSE

### Supply chain metrics
- Fill rate
- Stockout rate
- Food waste percentage
- Inventory turnover
- Gross profit

---

## Output Location

All generated outputs are saved in the `outputs/` folder.

Typical outputs include:

### Tables
- `forecast_metrics_table.csv`
- `forecast_comparison_detailed.csv`
- `feature_importance_table.csv`
- `kpi_comparison_table.csv`
- `kpi_comparison_transposed.csv`
- `result_summary_table.csv`
- `dataset_preparation_summary.csv`

### Plots
- `aggregate_weekly_demand_top10.png`
- `forecast_vs_actual_top_meal.png`
- `aggregate_forecast_vs_actual.png`
- `feature_importance_plot.png`
- `simulation_baseline_plot.png`
- `simulation_rf_plot.png`
- `food_waste_comparison.png`
- `fill_rate_comparison.png`
- `kpi_comparison_bar_chart.png`

These outputs are used in the final report and presentation.

---

## Notes

- The project uses relative paths and avoids hard-coded absolute paths.
- The system is designed as a single-echelon prototype for academic evaluation.
- Cost parameters and shelf-life assumptions are simplified for the prototype.
- The modular workflow allows future extension to multi-location or real-time systems.
