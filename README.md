# Food Delivery Data Analysis X Kagnus

[![Python Version](https://img.shields.io/badge/python-3.10%20%7C%203.11%20%7C%203.12%20%7C%203.13-blue.svg)](https://www.python.org/)
[![Project Status](https://img.shields.io/badge/status-Week%202%20Completed-success.svg)]()
[![License](https://img.shields.io/badge/license-Educational%20Use-lightgrey.svg)]()

> A four-week applied data analytics internship project supporting a hyper-local food delivery operations team to analyze fulfillment delays, optimize courier routing, and establish predictive operational intelligence.

---

## 📌 Project Overview
In modern on-demand food delivery networks (e.g., Swiggy, Zomato, DoorDash, Uber Eats), delivery duration (`Time_taken (min)`) is the single most critical determinant of customer retention, rider satisfaction, and platform profitability. 

This repository houses the end-to-end data analytics workflow completed across four progressive milestones:
- **Week 1: Dataset Understanding & Data Cleaning** *(Completed)*
- **Week 2: Exploratory Data Analysis (EDA) & Operational Comparisons** *(Current Milestone - Completed)*
- **Week 3: Advanced Business Metrics & Finalized Visualizations**
- **Week 4: Executive Insights, Fleet Recommendations & Final Reporting**

---

## 🗂️ Repository Structure

```
food-delivery-data-analysis/
├── data/
│   ├── raw/
│   │   ├── README.md                              # Raw dataset provenance, schema & immutability policy
│   │   └── food_delivery_raw.csv                  # Immutable original raw dataset (45,584 rows)
│   └── processed/
│       └── cleaned_food_delivery.csv              # Standardized, cleaned dataset (45,493 rows)
├── notebooks/
│   ├── 01_data_understanding_and_cleaning.ipynb   # Week 1: Data audit, cleaning pipeline & assertions
│   └── 02_exploratory_data_analysis.ipynb         # Week 2: Baseline metrics, factor comparisons & observations
├── visualizations/
│   └── initial_distance_vs_duration.png           # Week 2: Standalone high-res distance vs. duration scatter plot
├── docs/
│   └── cleaning_log.csv                           # Formal audit trail of issues, row counts & reasons
├── .gitignore                                     # Standard Python & Jupyter ignore rules
├── README.md                                      # Repository documentation & executive summaries
└── requirements.txt                               # External dependencies (pandas, numpy, matplotlib, seaborn)
```

### File Descriptions
- `data/raw/food_delivery_raw.csv`: Unmodified source data (45,584 rows × 20 columns).
- `data/processed/cleaned_food_delivery.csv`: Standardized, verified dataset (45,493 rows × 20 columns).
- `notebooks/01_data_understanding_and_cleaning.ipynb`: Week 1 notebook with 50 executed cells detailing data quality audits and cleaning assertions.
- `notebooks/02_exploratory_data_analysis.ipynb`: Week 2 notebook with 32 executed cells analyzing baseline metrics, operational factor comparisons, and evidence-based observations.
- `visualizations/initial_distance_vs_duration.png`: High-resolution scatter plot ($N = 41,863$) displaying Haversine distance versus delivery duration with OLS trendline.
- `docs/cleaning_log.csv`: Structured audit trail documenting 10 identified data defects and their remedies.
- `requirements.txt`: Minimal external Python dependencies.

---

## 🛠️ Technology Stack
- **Language**: Python 3.10+ (tested on Python 3.13)
- **Data Manipulation**: `pandas` (>= 2.0.0), `numpy` (>= 1.24.0)
- **Data Visualization**: `matplotlib` (>= 3.7.0), `seaborn` (>= 0.12.0)
- **Environment**: Jupyter Notebook / VS Code / Google Colab
- **Version Control**: Git & GitHub

---

## 🚀 Setup & Execution Instructions

```powershell
# 1. Clone repository
git clone https://github.com/Rajagopalasai/food-delivery-data-analysis.git
cd food-delivery-data-analysis

# 2. Install dependencies
pip install -r requirements.txt

# 3. Launch Week 2 Exploratory Analysis Notebook
jupyter notebook notebooks/02_exploratory_data_analysis.ipynb
```

---

## 📈 Week 2: Exploratory Data Analysis (EDA) Summary

### 1. Delivery-Duration Baseline Performance
Using the cleaned target column `Time_taken (min)` across **45,493 completed deliveries**:

| Metric | Calculated Value | Operational Meaning |
| :--- | :---: | :--- |
| **Sample Size ($N$)** | **45,493** | Total valid delivery records audited |
| **Mean ($\mu$)** | **26.30 minutes** | Network-wide average fulfillment time |
| **Median ($Q_2$)** | **26.00 minutes** | 50th percentile (50% faster, 50% slower) |
| **Std Deviation ($\sigma$)** | **9.39 minutes** | Overall operational dispersion around mean |
| **Minimum** | **10.00 minutes** | Fastest completed delivery |
| **25th Percentile ($Q_1$)** | **19.00 minutes** | Threshold for fastest quartile of fleet |
| **75th Percentile ($Q_3$)** | **32.00 minutes** | Threshold for slowest quartile of fleet |
| **Interquartile Range ($IQR$)** | **13.00 minutes** | Core middle-50% operational duration spread |
| **Maximum** | **54.00 minutes** | Slowest completed delivery (no corrupt 999 values) |
| **Skewness** | **+0.4857** | Mild rightward skew; nearly symmetric |
| **Kurtosis** | **-0.3117** | Platykurtic; slightly lighter tails than normal curve |

#### Operational SLA Tiers:
- **Fast / Express Fulfillment ($\le$ 30 min)**: **68.91%** ($N = 31,348$) — Excellent customer retention.
- **Standard Service Window (31–45 min)**: **27.93%** ($N = 12,708$) — Expected peak dining window.
- **Severe Delay / At-Risk Tier (> 45 min)**: **3.16%** ($N = 1,437$) — High cancellation risk.

---

### 2. Operational Factor Comparison Tables

#### A. Traffic Congestion Impact (`Road_traffic_density`)
| Traffic Density Tier | Delivery Count ($N$) | % of Total | Mean Duration (min) | Median Duration (min) | Std Dev (min) | Delta vs. Low (min) |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **Low** | 15,476 | 34.02% | **21.27** | 20.0 | 6.80 | Baseline |
| **Medium** | 10,945 | 24.06% | **26.70** | 27.0 | 8.56 | **+5.43 min (+25.5%)** |
| **High** | 4,423 | 9.72% | **27.24** | 27.0 | 8.40 | **+5.97 min (+28.1%)** |
| **Jam** | 14,139 | 31.08% | **31.18** | 31.0 | 9.94 | **+9.91 min (+46.6%)** |

#### B. Weather Conditions Impact (`Weather_conditions`)
| Weather Category | Delivery Count ($N$) | % of Total | Mean Duration (min) | Median Duration (min) | Std Dev (min) | Delta vs. Sunny (min) |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **Sunny** | 7,282 | 16.01% | **21.86** | 20.0 | 8.33 | Baseline |
| **Stormy** | 7,584 | 16.67% | **25.87** | 26.0 | 8.47 | **+4.01 min (+18.3%)** |
| **Sandstorms** | 7,494 | 16.47% | **25.88** | 26.0 | 8.62 | **+4.02 min (+18.4%)** |
| **Windy** | 7,422 | 16.31% | **26.12** | 26.0 | 8.62 | **+4.26 min (+19.5%)** |
| **Fog** | 7,653 | 16.82% | **28.91** | 28.0 | 10.13 | **+7.05 min (+32.3%)** |
| **Cloudy** | 7,533 | 16.56% | **28.92** | 28.0 | 10.09 | **+7.06 min (+32.3%)** |

#### C. Geospatial Distance Bins (`delivery_distance_km`)
- **Pearson Linear Correlation**: $r = \mathbf{+0.3206}$ (Moderate positive correlation)
- **Spearman Rank Correlation**: $\rho = \mathbf{+0.3196}$
- **Valid Telematics Trips**: $N = 41,863$ (3,630 rows had missing GPS sensor coordinates standardized to NaN in Week 1).

| Distance Bracket | Delivery Count ($N$) | % of Valid Trips | Mean Duration (min) | Median Duration (min) | Std Dev (min) | Delta vs. 0–5 km |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **0 – 5 km (Hyper-local)** | 11,279 | 26.94% | **22.19** | 21.0 | 7.41 | Baseline |
| **5 – 10 km (Core Urban)** | 11,286 | 26.96% | **24.39** | 25.0 | 8.01 | **+2.20 min (+9.9%)** |
| **10 – 15 km (Sub-urban)** | 11,270 | 26.92% | **29.85** | 29.0 | 9.82 | **+7.66 min (+34.5%)** |
| **15 – 20 km (Long Range)**| 6,240 | 14.90% | **29.89** | 29.0 | 9.83 | **+7.70 min (+34.7%)** |
| **20+ km (Periphery)** | 1,788 | 4.27% | **29.78** | 29.0 | 9.97 | **+7.59 min (+34.2%)** |

*Note the clear **Distance Plateau**: Beyond 10 km, mean duration flattens at ~29.8 minutes because couriers on long-range routes utilize arterial bypasses, while fixed food prep times (5–15 min) and traffic dominate short trips.*

#### D. Transit Mode & Vehicle Type (`Type_of_vehicle`)
| Vehicle Modality | Delivery Count ($N$) | % of Total Fleet | Mean Duration (min) | Median Duration (min) | Std Dev (min) |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **electric_scooter** | 3,778 | 8.30% | **24.48** | 24.0 | 8.62 |
| **scooter** | 15,241 | 33.50% | **24.48** | 24.0 | 8.70 |
| **bicycle** | 53 | 0.12% | **26.72** | 28.0 | 9.76 |
| **motorcycle** | 26,421 | 58.08% | **27.61** | 26.0 | 9.65 |

*Critique*: Electric and petrol scooters exhibit identical mean durations (24.48 min). Motorcycles average +3.13 min longer due to systematic algorithm assignment to longer routes. Bicycles ($N=53$, 0.12%) suffer from extreme sample sparsity and cannot be generalized.

#### E. Multiple Deliveries Batching Penalty (`multiple_deliveries`)
| Batched Stops | Delivery Count ($N$) | % of Orders | Mean Duration (min) | Median Duration (min) | Delta vs. 0 Stops |
| :---: | :---: | :---: | :---: | :---: | :---: |
| **0** | 14,056 | 30.90% | **22.88** | 22.0 | Baseline |
| **1** | 28,101 | 61.77% | **26.86** | 26.0 | **+3.98 min (+17.4%)** |
| **2** | 1,982 | 4.36% | **40.46** | 40.0 | **+17.58 min (+76.8%)** |
| **3** | 361 | 0.79% | **47.82** | 48.0 | **+24.94 min (+109.0%)** |

---

### 3. Six Evidence-Based Observations

1. **Severe Traffic Congestion (Jam) Imposes a ~10-Minute Fulfillment Penalty**:
   - `Jam` traffic ($N = 14,139$) averages **31.18 min** vs. **21.27 min** for `Low` traffic ($N = 15,476$), a **+9.91 min (+46.6%)** surcharge. Confounding factor: Jam traffic coincides with evening dinner peaks when restaurant kitchen queues are also at daily highs.
2. **Public Festivals Cause Network-Wide Delivery Delays**:
   - Festival deliveries ($N = 894$) average **45.52 min** (median: 45.0 min) vs. **25.99 min** (median: 25.0 min) on regular days ($N = 44,371$), an increase of **+19.53 min (+75.1%)**. Variance collapses ($\sigma = 4.01\min$), indicating universal systemic congestion.
3. **Batching Orders Beyond One Extra Stop Doubles Fulfillment Time**:
   - Single deliveries average **22.88 min**, adding 1 extra stop adds only **+3.98 min** (26.86 min), but stacking 2 stops escalates duration to **40.46 min (+76.8%)** and 3 stops to **47.82 min (+109.0%)**. Dispatch algorithms should strictly cap batching at 1 stacked delivery.
4. **Foggy and Cloudy Weather Outweighs Rain Storms in Delivery Latency**:
   - `Fog` (**28.91 min**) and `Cloudy` (**28.92 min**) add **+7.06 min (+32.3%)** over `Sunny` weather (**21.86 min**), creating greater persistent delay than rain storms (**25.87 min**), due to sustained visibility reduction across urban corridors.
5. **Distance Shows Moderate Correlation ($r = 0.3206$) and an Urban Distance Plateau**:
   - Physical distance explains only $\sim 10.3\%$ ($R^2 = 0.103$) of duration variance. Fixed kitchen prep times (5–15 min) and traffic signals dominate short trips (< 5 km), while trips beyond 10 km utilize arterial bypasses and plateau at ~29.8 minutes.
6. **Customer Ratings Strongly Predict Delivery Speed, While Vehicle Types Show Parity**:
   - Couriers with low ratings ($< 4.0$, $N = 1,329$) average **37.14 min**, while top-rated couriers ($\ge 4.5$, $N = 35,562$) average **24.3 min** (a **+12.8 min / +52.3%** delay gap). Confounding factor: Two-way causality—delivery delays cause customer down-voting.

---

### 4. Dataset Limitations & Unavailable Fields
- **Courier Experience**: The dataset contains no explicit `years_of_experience` or `tenure` column. Courier age brackets and rating tiers were utilized as empirical proxy indicators.
- **Missing Sensor Coordinates**: 3,630 rows (~7.98%) had missing GPS sensor coordinates (0.0, 0.0) from raw telematics drops. They were excluded from spatial distance calculations but retained for non-spatial factor analyses.
- **Bicycle Sample Size**: Bicycles account for only 53 deliveries (0.12%), precluding statistically reliable generalizations regarding human-powered transit modes.

---

## 🗺️ Next Steps: Week 3 Roadmap
- Design the **five finalized publication-grade operational charts**.
- Target visualizations for: Traffic Delay Tiers, Weather Latency Impact, Distance Plateau Scatter, Multi-Stop Batching Escalation, and Rating vs. Duration Performance.
- Formulate concrete business recommendations and fleet optimization frameworks.

---

## 👤 Author & Academic Integrity
- **Role**: Junior Data Analyst (Operations Analytics)
- **Program**: Kagnus Data Analytics Training & Internship
- **Verification**: All numerical metrics, percentages, and deltas were calculated directly from code execution on the cleaned dataset without fabrication.
