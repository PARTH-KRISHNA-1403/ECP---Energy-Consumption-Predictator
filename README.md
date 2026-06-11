# ECP---Energy-Consumption-Predictator
## India State-Wise Electricity Generation Predictor

It's a machine learning pipeline to forecast monthly electricity generation (in Gigawatt-Hour / GWh) across different states and union territories in India. 

Instead of treating the forecasting problem as a blind mathematical formula, it uses historical "momentum" (lag features) and regional weather patterns (Indian seasons) to help utility companies, grid managers, and businesses better anticipate regional energy trends.

---

## 📊 The Dataset

The project uses historical indian grid metrics from January 2019 to November 2025. It details:
* **The Target Variable:** `Total Generation` (GWh) which serves as our proxy for energy demand.
* **Geographic Scale:** Filtered data points capturing individual Indian states (e.g., Maharashtra, Tamil Nadu) while stripping out macro national totals.
* **Time Scale:** Logged on the 1st of every month.

---

## ⚙️ How It Works (Feature Engineering)

To make a standard machine learning algorithm understand time-series data without breaking down, we extract and create three main kinds of features:

1. **Calendar Fields:** We pull the `Month` and `Year` integers directly from the timestamps.
2. **Indian Meteorological Seasons:** Months are mapped into four true seasonal buckets to capture heavy climate shifts (e.g., massive air conditioning demands during high Summer heat):
   * **Winter** (Dec, Jan, Feb)
   * **Summer** (Mar, Apr, May)
   * **Monsoon** (Jun, Jul, Aug, Sep)
   * **Post-Monsoon** (Oct, Nov)
3. **Lag Features (`Lag_1` & `Lag_12`):** This is the secret sauce. We feed the model what a specific state generated exactly 1 month ago (capturing recent momentum) and exactly 12 months ago (capturing annual cyclical trends).

---

## 🤖 Models Trained

We split the data strictly by time to test our models fairly:
* **Training Set:** Everything from 2020 through December 2024.
* **Testing Set:** Jan 2025 – Nov 2025 (used as "unseen" future data).

We compare two models:
1. **Linear Regression:** A simple baseline model that checks for steady linear growth.
2. **Random Forest Regressor:** An advanced tree-based model that effortlessly picks up non-linear shifts (like extreme heat waves in summer) and relative rules rather than absolute numbers.

---

## 📈 Results & Visualizations

Both models perform incredibly well, pulling an accuracy ($R^2$) score of over **99%**. 


---

## Prerequisites
Make sure you have Python installed, along with the necessary data science frameworks:
```bash
pip install pandas scikit-learn matplotlib
```

## File Organization
├── india_monthly_full_release_long_format.csv \
└── predict_energy.py

## Execution
```Bash
python predict_energy.py
```


