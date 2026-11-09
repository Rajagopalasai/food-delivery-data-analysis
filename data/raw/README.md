# Raw Dataset Documentation: Food Delivery Operations

## 1. Overview & Source
- **Dataset Name**: Food Delivery Dataset (`food_delivery_raw.csv`)
- **Origin / Provider**: Kagnus Data Analytics Training & Internship Program / Kaggle Food Delivery Dataset
- **Domain**: Hyper-local On-Demand Food Delivery Operations (India)
- **Timeframe Covered**: February 11, 2022 to April 06, 2022 (44 distinct operational dates)
- **Initial Dimensions**: 45,584 rows × 20 columns
- **File Format**: Comma-Separated Values (CSV), UTF-8 encoded
- **License**: Provided for educational and analytic training purposes under standard public educational benchmark dataset terms.

---

## 2. Access & Acquisition Instructions
If downloading from external sources or reproducing the project setup:
1. Obtain the source CSV titled `Food delivery Dataset.csv` from the official Kagnus portal or repository resources.
2. Place the unmodified source file into `data/raw/` with filename `food_delivery_raw.csv`.
3. Verify that the SHA-256 hash or row count matches **45,584 rows** and **20 columns** prior to executing the processing pipeline.

---

## 3. Immutability Policy
In strict accordance with analytical and reproducible data engineering standards:
- The contents of `data/raw/` are **read-only and immutable**.
- No cleaning, filtering, sorting, or value imputation should ever be performed directly on raw files.
- All downstream transformations are saved exclusively to `data/processed/cleaned_food_delivery.csv`.

---

## 4. Column Schema & Descriptions

| Column Name | Raw Data Type | Description | Example / Range |
| :--- | :--- | :--- | :--- |
| `ID` | String / Object | Unique hexadecimal delivery order identifier | `0xcdcd`, `0xd987` |
| `Delivery_person_ID` | String / Object | Delivery partner / route identifier encoding city, restaurant, and slot | `DEHRES17DEL01`, `BANGRES05DEL01` |
| `Delivery_person_Age` | Float64 | Age of the delivery partner in years | 15.0 to 50.0 (Valid operational: 20–39) |
| `Delivery_person_Ratings` | Float64 | Customer rating / average rating of delivery partner | 1.0 to 6.0 (Valid scale: 1.0–5.0) |
| `Restaurant_latitude` | Float64 | GPS latitude of restaurant pick-up location | -30.91 to +30.91 (Includes 0.0 placeholders & negative signs) |
| `Restaurant_longitude` | Float64 | GPS longitude of restaurant pick-up location | -88.43 to +88.43 (Includes 0.0 placeholders & negative signs) |
| `Delivery_location_latitude` | Float64 | GPS latitude of customer delivery drop-off location | 0.01 to 31.05 |
| `Delivery_location_longitude` | Float64 | GPS longitude of customer delivery drop-off location | 0.01 to 88.56 |
| `Order_Date` | String / Object | Date when the food order was placed (`DD-MM-YYYY`) | `12-02-2022`, `04-03-2022` |
| `Time_Orderd` | String / Object | Timestamp of order placement (mixed formats & day fractions) | `21:55`, `0.458333333` |
| `Time_Order_picked` | String / Object | Timestamp when order was picked up by rider | `22:10`, `24:05:00` |
| `Weather_conditions` | String / Object | Ambient atmospheric condition during delivery | `Fog`, `Stormy`, `Cloudy`, `Sunny`, etc. |
| `Road_traffic_density` | String / Object | Traffic congestion level at the time of delivery | `Low`, `Medium`, `High`, `Jam` |
| `Vehicle_condition` | Int64 | Condition score of rider's vehicle | 0 (poor), 1 (fair), 2 (good), 3 (excellent) |
| `Type_of_order` | String / Object | Meal category ordered | `Snack`, `Meal`, `Drinks`, `Buffet` |
| `Type_of_vehicle` | String / Object | Vehicle mode used for delivery | `motorcycle`, `scooter`, `electric_scooter`, `bicycle` |
| `multiple_deliveries` | Float64 | Number of additional deliveries batched with the order | 0.0, 1.0, 2.0, 3.0 |
| `Festival` | String / Object | Flag indicating whether order occurred during a public festival | `No`, `Yes` |
| `City` | String / Object | Urbanization zone of the delivery area | `Metropolitian`, `Urban`, `Semi-Urban` |
| `Time_taken (min)` | Int64 | Target variable: total duration from order placement to delivery | 10 to 54 minutes |
