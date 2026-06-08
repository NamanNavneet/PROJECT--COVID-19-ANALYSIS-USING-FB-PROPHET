# 🦠 Covid-19 Pandemic Analysis and Prediction

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/NamanNavneet/MAJOR-PROJECT/blob/gh-pages/Covid19PandemicAnalysisandPrediction.ipynb)
![Python](https://img.shields.io/badge/Python-3.7-blue)
![Prophet](https://img.shields.io/badge/Facebook-Prophet-orange)
![License](https://img.shields.io/badge/License-MIT-green)
![Dataset](https://img.shields.io/badge/Dataset-Our%20World%20In%20Data-red)

A comprehensive **time-series analysis and forecasting project** on the Covid-19 pandemic using Facebook Prophet. The project covers global and country-level trends across cases, deaths, and vaccinations — with detailed case studies on India, the United States, and age-group demographics.

---

## 📌 Project Overview

This major data science project analyzes the Covid-19 pandemic using real-world global data. It answers key epidemiological questions through exploratory data analysis, statistical summaries, and future trend forecasting using Facebook's Prophet time-series model.

**3 Core Analysis Sections:**

| Section | Description |
|---|---|
| 📊 Overview | Global total cases, deaths, vaccinations |
| 👴 Case Study I | Age group analysis (Median age, 65+, 70+) |
| 🌍 Case Study II | Country-level deep dive (India & United States) |
| 🆕 Case Study III (Optional) | New dataset: New Cases, New Deaths, New Vaccinations |

---

## 📂 Dataset

**Source:** [Our World in Data — COVID-19 Dataset](https://ourworldindata.org/covid-deaths)

- **File:** `owid-covid-data2.csv` (main) and `owid-covid-data.csv` (optional section)
- **Coverage:** Global, from February 2020 to July 2021
- **Key Columns Used:**

| Column | Description |
|---|---|
| `location` | Country name |
| `date` | Date of record |
| `total_cases` | Cumulative confirmed cases |
| `total_deaths` | Cumulative deaths |
| `total_vaccinations` | Cumulative vaccinations |
| `new_cases` | New daily cases |
| `new_deaths` | New daily deaths |
| `new_vaccinations` | New daily vaccinations |
| `median_age` | Median age of country population |
| `aged_65_older` | % population aged 65+ |
| `aged_70_older` | % population aged 70+ |

> 📥 **Download Dataset:** Upload `owid-covid-data2.csv` to your Colab runtime or Google Drive before running.

---

## 🔧 Tech Stack

| Component | Tool/Library |
|---|---|
| Language | Python 3.7 |
| Time-Series Forecasting | Facebook Prophet (`fbprophet`) |
| Data Manipulation | Pandas, NumPy |
| Visualization | Matplotlib, Seaborn |
| Notebook Environment | Google Colab / Jupyter |
| Timing | `ipython-autotime` |

---

## 🚀 Project Structure & Workflow

```
covid19-analysis/
│
├── Covid_19_Pandemic_Analysis_and_Prediction.ipynb  # Main notebook
├── owid-covid-data2.csv                              # Primary dataset
├── owid-covid-data.csv                               # Optional dataset (Case Study III)
└── README.md
```

---

## 📋 Analysis Sections

### 1. 🔧 Installation & Setup
```python
!pip install fbprophet ipython-autotime
from google.colab import drive
drive.mount('/content/drive')
```

### 2. 📊 Overview — Global Analysis
Exploratory analysis on aggregated global data:
- **Q1:** Country with highest number of Covid-19 cases → **United States (33,717,567)**
- **Q2:** Country with lowest cases → **Afghanistan (1)**
- **Q3:** Country with highest deaths → **United States (605,526)**
- **Q4:** Country with lowest deaths → **Afghanistan (1)**
- **Q5:** Most vaccinated country → **China (1,305,499,000)**
- **Q6:** Least vaccinated country → **Afghanistan (0)**
- **Q7:** Date of highest cases → **April 7, 2021**
- **Q8:** Date of lowest cases → **February 24, 2020**
- **Q9:** Date of highest deaths → **April 7, 2021**
- **Q10:** Date of lowest deaths → **March 22, 2020**
- **Q11:** Date of maximum vaccinations → **April 7, 2021**
- **Q12:** Date of minimum vaccinations → **February 22, 2021**
- **Q13:** Mean total cases per country → **355,088**
- **Q14:** Mean total deaths per country → **9,572**
- **Q15:** Mean total vaccinations per country → **10,833,540**

### 3. 🔮 Time-Series Forecasting with Facebook Prophet
For each metric (cases, deaths, vaccinations), the workflow is:

```python
# Step 1 — Prepare data in Prophet format (ds = date, y = value)
df_prophet = df[['Date', 'Number of Cases']].rename(columns={'Date': 'ds', 'Number of Cases': 'y'})

# Step 2 — Fit the model
model = Prophet()
model.fit(df_prophet)

# Step 3 — Make future dataframe and predict
future = model.make_future_dataframe(periods=365)
forecast = model.predict(future)

# Step 4 — Plot forecast
model.plot(forecast)
model.plot_components(forecast)
```

**Cross-Validation & Performance Metrics:**
```python
from fbprophet.diagnostics import cross_validation, performance_metrics
df_cv = cross_validation(model, initial='180 days', period='90 days', horizon='365 days')
df_p = performance_metrics(df_cv)
```

Metrics evaluated: **MAE, RMSE, MAPE, Coverage**

### 4. 👴 Case Study I — Age Group Analysis
Forecasting trends segmented by demographic vulnerability:
- **Median Age Group** — Global case trends by median country age
- **Aged 65+** — Cases and deaths for elderly population (65 years and older)
- **Aged 70+** — Cases and deaths for elderly population (70 years and older)

Bar charts plotted for **Age vs. Location** to visualize geographic vulnerability patterns.

### 5. 🌍 Case Study II — Country Analysis

**India 🇮🇳**
- Total cases, deaths, vaccination trend analysis
- Prophet forecasting for 365 days ahead
- Cross-validation with performance metrics (MAE, RMSE, MAPE)

**United States 🇺🇸**
- Same pipeline applied to US-specific data
- Forecast plots with uncertainty intervals
- Component plots (trend + weekly seasonality)

### 6. 🆕 Case Study III (Optional) — New Dataset Analysis
Uses updated `owid-covid-data.csv` to analyze:
- **New Cases** per day
- **New Deaths** per day
- **New Vaccinations** per day

Separate Prophet models trained and forecasted for each metric.

---

## 📊 Key Findings

| Insight | Value |
|---|---|
| Highest cases country | United States (33.7M) |
| Highest vaccinations country | China (1.3B doses) |
| Peak global case date | April 7, 2021 |
| Mean cases per country | ~355,088 |
| Mean vaccinations per country | ~10.8M |
| Forecast horizon | 365 days |

---

## ⚙️ Setup & Run

### Option 1 — Google Colab (Recommended)
1. Click the **Open in Colab** badge above
2. Upload `owid-covid-data2.csv` to your Colab session or mount Google Drive
3. Run all cells sequentially

### Option 2 — Local Setup
```bash
# Clone the repository
git clone https://github.com/NamanNavneet/MAJOR-PROJECT.git
cd MAJOR-PROJECT

# Install dependencies
pip install fbprophet pandas numpy matplotlib seaborn ipython-autotime

# Launch notebook
jupyter notebook Covid_19_Pandemic_Analysis_and_Prediction.ipynb
```

> ⚠️ **Note:** `fbprophet` installation may require `pystan`. Use Python 3.7 for best compatibility. On newer Python, use `prophet` (the updated package name).

```bash
pip install prophet  # for Python 3.8+
```

---

## 💡 Key Learnings

- End-to-end time-series analysis pipeline on real-world pandemic data
- Data preprocessing and handling missing values in large multi-country datasets
- Using Facebook Prophet for trend forecasting with uncertainty quantification
- Cross-validation for time-series models and evaluating MAE, RMSE, MAPE
- Demographic segmentation and comparative country-level analysis
- Data visualization for time-series trends and geographic patterns

---

## 🔮 Future Improvements

- [ ] Add interactive visualizations using Plotly or Bokeh
- [ ] Incorporate vaccination impact on forecasted death rates
- [ ] Build a Streamlit dashboard for real-time exploration
- [ ] Add LSTM/Transformer-based forecasting for comparison
- [ ] Extend dataset to 2022–2024 for Omicron wave analysis

---

## 👤 Author

**Naman Navneet**
- 🔗 [LinkedIn](https://www.linkedin.com/in/naman-navneet)
- 💻 [GitHub](https://github.com/NamanNavneet)

---

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).
