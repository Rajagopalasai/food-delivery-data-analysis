# Food Delivery Data Analysis X Kagnus

[![Python Version](https://img.shields.io/badge/python-3.10%20%7C%203.11%20%7C%203.12%20%7C%203.13-blue.svg)](https://www.python.org/)
[![Project Status](https://img.shields.io/badge/status-Week%201%20Completed-success.svg)]()
[![License](https://img.shields.io/badge/license-Educational%20Use-lightgrey.svg)]()

> A four-week applied data analytics internship project supporting a hyper-local food delivery operations team to analyze fulfillment delays, optimize courier routing, and establish predictive operational intelligence.

---

## 📌 Project Overview
In modern on-demand food delivery networks (e.g., Swiggy, Zomato, DoorDash, Uber Eats), delivery duration (`Time_taken (min)`) is the single most critical determinant of customer retention, rider satisfaction, and platform profitability. 

This repository houses the end-to-end data analytics workflow completed across four progressive milestones:
- **Week 1: Dataset Understanding & Data Cleaning** *(Current Milestone)*
- **Week 2: Exploratory Data Analysis (EDA) & Operational Visualizations**
- **Week 3: Advanced Business Metrics & Operational Deep-Dives**
- **Week 4: Final Executive Insights, Dashboard & Reporting**

---

## 🎯 Week 1 Objectives & Deliverables
As a junior data analyst supporting the food-delivery operations team, the Week 1 mandate is to transform raw, noisy operational telematics into an audited, standardized, and dependable analytical dataset:
1. **Load & Understand**: Inspect the 45,584-row, 20-column transaction dataset, define feature purposes, and document what one row represents.
2. **Quality Audit**: Systematically test for missing values, duplicates, categorical misspellings, negative coordinates, out-of-scale ratings, and corrupted spreadsheet timestamps.
3. **Evidence-Based Cleaning**: Execute a transparent, defensible cleaning pipeline on a separate DataFrame without altering the raw dataset or inventing artificial data.
4. **Verification & Audit Trail**: Document every modification in `docs/cleaning_log.csv`, export the clean dataset to `data/processed/cleaned_food_delivery.csv`, and verify the final artifact with automated assertions.

---

## 🗂️ Repository Structure

```
food-delivery-data-analysis/
├── data/
│   ├── raw/
│   │   ├── README.md                          # Raw dataset provenance, schema & immutability policy
│   │   └── food_delivery_raw.csv              # Immutable original raw dataset (45,584 rows)
│   └── processed/
│       └── cleaned_food_delivery.csv          # Standardized, cleaned dataset (45,493 rows)
├── notebooks/
│   └── 01_data_understanding_and_cleaning.ipynb # Fully documented & executed Jupyter Notebook
├── docs/
│   └── cleaning_log.csv                       # Formal audit trail of issues, row counts, & rationale
├── README.md                                  # Root repository documentation and project guide
└── requirements.txt                           # External Python dependencies for reproducibility
```

### File Descriptions
- `data/raw/README.md`: Documents the source, license, schema, and read-only policy for raw data files.
- `data/raw/food_delivery_raw.csv`: The unmodified, original dataset containing 45,584 rows and 20 columns.
- `data/processed/cleaned_food_delivery.csv`: The finalized, verified analytical dataset (45,493 rows × 20 columns).
- `notebooks/01_data_understanding_and_cleaning.ipynb`: Comprehensive notebook structured with pre-code explanations, markdown tables, executed Python code, diagnostic visualizations, and post-execution business interpretations.
- `docs/cleaning_log.csv`: Structured audit trail recording issue description, affected column(s), affected row counts, cleaning action taken, and operational justification.
- `requirements.txt`: Minimal pinned external Python dependencies (`pandas`, `numpy`, `matplotlib`, `seaborn`, `jupyter`).

---

## 🛠️ Technology Stack
- **Language**: Python 3.10+ (tested on Python 3.13)
- **Data Manipulation**: `pandas` (>= 2.0.0), `numpy` (>= 1.24.0)
- **Data Visualization**: `matplotlib` (>= 3.7.0), `seaborn` (>= 0.12.0)
- **Environment**: Jupyter Notebook / VS Code / Google Colab
- **Version Control**: Git & GitHub

---

## 🚀 Setup & Execution Instructions

### Option A: Local Environment (VS Code / Terminal)

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/<your-username>/food-delivery-data-analysis.git
   cd food-delivery-data-analysis
   ```

2. **Create and Activate a Virtual Environment**:
   ```bash
   # Windows PowerShell
   python -m venv venv
   .\venv\Scripts\Activate.ps1

   # macOS / Linux
   python3 -m venv venv
   source venv/bin/activate
   ```

3. **Install Dependencies**:
   ```bash
   pip install --upgrade pip
   pip install -r requirements.txt
   ```

4. **Launch the Notebook**:
   ```bash
   jupyter notebook notebooks/01_data_understanding_and_cleaning.ipynb
   ```
   *Alternatively, open the repository folder in VS Code and select the `venv` kernel.*

### Option B: Google Colab
1. Upload `notebooks/01_data_understanding_and_cleaning.ipynb` to Google Colab.
2. Upload `food_delivery_raw.csv` into a folder named `data/raw/` in the Colab file explorer.
3. Run all cells sequentially from top to bottom.

---

## 📊 Summary of Week 1 Findings & Cleaning Decisions

### 1. What One Row Represents
Each row captures **one completed food delivery order fulfillment cycle** across major Indian municipalities (e.g., Bangalore, Mumbai, Pune, Delhi, Jaipur, Chennai) between February 11, 2022, and April 06, 2022. It tracks the courier assignment, partner demographics, pickup restaurant coordinates, drop-off location coordinates, order placement timestamp, courier pickup timestamp, environmental factors (weather, traffic), vehicle condition, batch size, and the target delivery duration in minutes (`Time_taken (min)`).

### 2. Key Data Quality Defects Identified & Resolved

| # | Data Quality Defect | Affected Rows | Resolution Action | Operational Rationale |
| :-: | :--- | :-: | :--- | :--- |
| **1** | **Synthetic / Corrupted Test Records** | 91 rows | **Excluded records** | Contained out-of-scale ratings (`6.0`), sentinel ages (`15.0` & `50.0`), and 100% missing order time, weather, and traffic data. |
| **2** | **Negative Restaurant Latitudes** | 399 rows | **Corrected via `abs()`** | Inverted sign during entry. India is strictly in the Northern Hemisphere (+8° to +37° N). Delivery latitudes were positive and matching. |
| **3** | **Negative Restaurant Longitudes** | 135 rows | **Corrected via `abs()`** | Inverted sign during entry. India is strictly in the Eastern Hemisphere (+68° to +97° E). Delivery longitudes were positive and matching. |
| **4** | **GPS Sensor 0.0 Placeholders (Null Island)** | 3,630 rows | **Standardized to `NaN`** | (0.0, 0.0) coordinates represent device GPS drops. Setting to `NaN` prevents false 0 km or 8,000 km distances while preserving valid operational trip data. |
| **5** | **Excel Day Fraction Timestamps** | 43,853 rows | **Standardized to `HH:MM:SS`** | Spreadsheet exports converted times to fractions of a 24-hr day (e.g. `0.458333333` = 11:00:00). Converted using `round(val * 86400)`. |
| **6** | **Midnight Hour Formatting Error** | 45,493 rows | **Standardized to `HH:MM:SS`** | Remapped midnight timestamps formatted as `24:05:00` to standard 24-hour `00:05:00`. |
| **7** | **Category Spelling Typo** | 34,023 rows | **Standardized spelling** | Replaced `'Metropolitian'` typo with standard English `'Metropolitan'`. |
| **8** | **Ambiguous Date Format** | 45,493 rows | **Converted to ISO 8601** | Converted day-first string `'DD-MM-YYYY'` to standard `'YYYY-MM-DD'`. |
| **9** | **Float Cast for Discrete Count** | 44,500 rows | **Cast to `Int64`** | Converted `multiple_deliveries` from float to nullable integer to eliminate decimals (e.g. `1` instead of `1.0`). |
| **10**| **Missing Demographic/Context Values** | 510–1,908 rows | **Retained as `NaN`** | Missing at random across cities and couriers. Retained without artificial imputation to prevent synthetic variance bias. |

### 3. Before-and-After Row Count & Dimension Comparison

| Metric | Raw Dataset (`df`) | Cleaned Dataset (`df_cleaned`) | Delta / Difference | Explanation |
| :--- | :---: | :---: | :---: | :--- |
| **Total Rows** | 45,584 | **45,493** | **-91 rows (-0.20%)** | Removal of 91 corrupted dummy test records |
| **Total Columns** | 20 | **20** | **0** | Original schema fully preserved |
| **Ratings > 5.0** | 53 | **0** | -53 | Elimination of impossible 6.0 ratings |
| **Ages < 18 or > 49** | 91 | **0** | -91 | Removal of sentinel 15.0 and 50.0 ages |
| **Negative Coordinates** | 593 | **0** | -593 | Inverted signs corrected with absolute value |
| **Invalid 0.0 Coordinates** | 3,640 | **0** | -3,640 | Replaced placeholder zeroes with explicit `NaN` |
| **Typo: 'Metropolitian'** | 34,087 | **0** | -34,087 | Standardized to 'Metropolitan' |
| **Date Format** | DD-MM-YYYY | **YYYY-MM-DD** | Standardized | ISO 8601 compliance |

---

## 🔍 Assumptions & Operational Limitations
1. **GPS Coordinates (0.0, 0.0)**: Exactly 3,630 rows (~7.98% of clean data) have missing GPS coordinates. Because their operational delivery durations, order categories, and traffic densities are valid and uncorrupted, these rows are retained with coordinates set to `NaN`. Downstream spatial models must filter or account for missing spatial features.
2. **Missing Demographic Values**: Missing values in `Delivery_person_Age` (1,854 nulls) and `Delivery_person_Ratings` (1,908 nulls) occur at random across different couriers and regions. Rather than inventing arbitrary values (mean/mode), they are preserved as `NaN` to maintain honesty and prevent false variance suppression.
3. **Kitchen Preparation Times**: Mathematical inspection revealed that kitchen preparation duration (`Time_Order_picked` minus `Time_Orderd`) is strictly quantized into 5, 10, or 15-minute intervals across all merchants, reflecting platform dispatch timer buckets.

---

## 🗺️ Next Steps: Week 2 Roadmap
With an immutable raw data repository, a defensible cleaning log, and a verified processed dataset in place, **Week 2** will proceed directly to:
- Univariate distribution analyses of order delivery times across urban markets.
- Bivariate evaluations of weather severity (e.g. Stormy vs. Fog) and traffic density on fulfillment delays.
- Multi-delivery batching efficiency analysis.
- Production of the five core executive operational visualizations.

---

## 👤 Author & Academic Integrity
- **Role**: Junior Data Analyst (Operations Analytics)
- **Program**: Kagnus Data Analytics Training & Internship
- **Verification**: All numbers, row counts, and percentages documented in this repository were computed directly from code execution on the original dataset without fabrication.
