# Hunt_Digital_Media_assignment
# 🚦 Invalid Traffic (IVT) Detection & Analysis

This project analyzes traffic data from multiple apps to identify patterns of **Invalid Traffic (IVT)** — i.e., fake or bot-generated activity — and compares it with normal traffic to understand behavioral differences.

---

## 📊 Project Overview

We have data from **3 apps marked with IVT** and **3 apps without IVT**.
The goal is to analyze:

* Why certain apps show invalid traffic patterns
* When (time/day) suspicious activity peaks
* What differentiates IVT-marked apps from normal ones

---

## 🧠 Objectives

1. **Compare** key metrics between IVT and non-IVT apps
2. **Identify** abnormal behavior using ratios and request patterns
3. **Analyze** temporal patterns (hourly & daily) to spot bot-like activity
4. **Generate** visual and statistical evidence supporting IVT classification

---

## ⚙️ Steps Performed

### 1. **Data Preparation**

* Loaded and cleaned hourly app-level traffic data
* Extracted timestamps into `hour_of_day` and `day_of_week`
* Defined threshold-based binary flag:

  ```python
  df['ivt_flagged'] = (df['idfa_ua_ratio'] > 2000).astype(int)
  ```

### 2. **Feature Engineering**

Added meaningful features:

* `ivt_flagged` → Binary IVT indicator
* `hour_of_day`, `day_of_week` → For temporal trend analysis

### 3. **Statistical Summary**

Generated metrics summary (`summary_table_IVT_vs_Normal.csv`) comparing:

* `idfa_ua_ratio`
* `requests_per_idfa`
* `idfa_ip_ratio`

### 4. **Visualization**

Created and saved insightful plots in the `plots/` folder:

* Boxplots comparing IVT vs Normal traffic
* Time series trends of key metrics
* Bar plots showing IVT spikes by hour and day

---

## 📈 Key Insights

* **IVT traffic** has **very high `idfa_ua_ratio`**, indicating many devices share the same user-agent → a red flag for automation.
* **Requests per IDFA** slightly higher for IVT, consistent with bot-generated volume.
* **Temporal spikes** show fake activity peaks during specific **hours** and **days**, revealing possible scripted traffic cycles.
* Normal apps maintain stable and consistent behavior across time.

---

## 🧠 Conclusion

* Apps with high **IDFA–UA ratios (>2000)** consistently show IVT behavior.
* IVT traffic displays **time-based clustering**, suggesting non-human traffic bursts.
* The combined metric and time analysis offers a **data-driven way to detect fake activity**.

This framework can be extended for **real-time fraud monitoring**, threshold automation, and advanced anomaly detection.
