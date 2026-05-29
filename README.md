
# 🚖 Uber NYC Pickup Analysis
### Exploratory Data Analysis · Python · Plotly · Folium

![Python](https://img.shields.io/badge/Python-3.9-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![Plotly](https://img.shields.io/badge/Plotly-3F4F75?style=for-the-badge&logo=plotly&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)


---

## 📌 Overview
https://nbviewer.org/github/Austin-1912/uber-data-analysis-nyc/blob/main/uber_analysis_austin_mathew_1.ipynb
This project explores **15M+ Uber pickup records** across New York City spanning 2014–2015. The goal is to uncover demand patterns that answer three core questions:

- 📅 **When** does demand peak — by month, weekday, and hour?
- 📍 **Where** do rides concentrate across the city?
- 🚏 **Which** dispatch bases and airports drive the most volume?

---

## 📂 Datasets

| File | Description |
|------|-------------|
| `uber-raw-data-janjune-15_sample.csv` | ~1M sampled pickups, Jan–Jun 2015 |
| `uber-raw-data-apr14.csv` → `sep14.csv` | Monthly raw pickups, Apr–Sep 2014 |
| `Uber-Jan-Feb-FOIL.csv` | Active vehicle counts per dispatch base (FOIL data) |

> The full Jan–Jun 2015 dataset contains ~15 million rows. The sample (~1M rows) is used for performance.

---

## 🔍 Analysis Breakdown

### 1 · Data Cleaning & Preparation
- Removed duplicate rows using `.duplicated()` and `.drop_duplicates()`
- Converted `Pickup_date` from `object` → `datetime64` via `pd.to_datetime()`
- Extracted time features: `month`, `weekday`, `day`, `hour`, `minute`

### 2 · Monthly & Weekday Demand
- Cross-tab pivot (`pd.crosstab`) of pickups by **Month × Weekday**
- Visualised as a **grouped bar chart** using Plotly Express

### 3 · Hourly Rush by Day of Week
- Grouped pickups by `['weekday', 'hour']` with proper categorical sorting
- Plotted as a **multi-line chart** across all 24 hours

### 4 · Pareto Analysis — Dispatch Bases
- Calculated each base's share of total trips and cumulative percentage
- Dual-axis **Pareto chart** (bar + line) with 80% threshold marker

### 5 · Airport Demand Analysis
- Filtered pickups by LocationID for **EWR, JFK, and LGA**
- **Area chart** showing hourly demand pressure per airport

### 6 · Geographic Hotspot Mapping
- **Static heatmap** (`folium.HeatMap`) — full pickup density across NYC
- **Animated heatmap** (`HeatMapWithTime`) — hourly demand movement on a CartoDB basemap

### 7 · Day × Hour Pivot Heatmap
- Built with `.groupby(['day','hour']).size().unstack()`
- Styled with Pandas `.style.background_gradient()` for instant pattern recognition

### 8 · Reusable Analysis Function
- Wrapped pivot logic into `gen_pivot_table(df, col1, col2)` for flexible pairwise analysis

---

## 📊 Visualisations

| Chart | Library | Purpose |
|-------|---------|---------|
| Grouped Bar Chart | Plotly Express | Monthly pickups × weekday |
| Multi-Line Chart | Plotly Express | Hourly rush by day of week |
| Pareto Chart | Plotly Graph Objects | Dispatch base trip share |
| Area Chart | Plotly Express | Airport hourly demand |
| Static Heatmap | Folium | Geographic pickup density |
| Animated Heatmap | Folium (HeatMapWithTime) | Hourly demand movement |
| Gradient Pivot | Pandas Styler | Day × Hour rush matrix |
| Box & Violin | Plotly Express | Active vehicles per base |

---

## 💡 Key Insights

**Monthly & Weekly Demand**
> June has the highest pickup volume in the 2015 sample. Fridays and Saturdays dominate demand across every month.

**Hourly Patterns**
> Saturday and Sunday follow similar morning trends but diverge sharply in the evening — Saturday climbs all night while Sunday drops off early. Thursday nights mirror Friday/Saturday levels, suggesting New Yorkers effectively start their weekend on Thursday.

**Dispatch Bases (Pareto)**
> A minority of dispatch bases account for ~80% of all trips — a clear Pareto distribution in ride-hailing operations.

**Airport Demand**
> JFK and LGA lead in volume. All three airports (EWR, JFK, LGA) spike during early morning and evening hours, aligned with peak flight windows.

**Geographic Hotspots**
> Midtown Manhattan is the dominant hotspot. High-density corridors extend south to Lower Manhattan, with secondary clusters in Upper Manhattan and the Heights of Brooklyn.

---

## 🛠 Tech Stack

| Tool | Version | Use |
|------|---------|-----|
| Python | 3.9 | Core language |
| Pandas | Latest | Data wrangling & pivot tables |
| NumPy | Latest | Numerical operations |
| Plotly Express | Latest | Interactive charts |
| Plotly Graph Objects | Latest | Custom dual-axis Pareto chart |
| Folium | Latest | Interactive geographic maps |
| Seaborn / Matplotlib | Latest | Supplementary plots |
| Jupyter Notebook | Latest | Development environment |

---

## ▶️ How to Run

**1. Clone the repository**
```bash
git clone https://github.com/YOUR_USERNAME/uber-data-analysis-nyc.git
cd uber-data-analysis-nyc
```

**2. Install dependencies**
```bash
pip install pandas numpy plotly folium seaborn matplotlib jupyter
```

**3. Add your datasets**

Place all CSV files in the same folder as the notebook, or update `DATA_PATH` in the first cell.

**4. Launch the notebook**
```bash
jupyter notebook uber_analysis_austin_mathew.ipynb
```

**5. Run all cells**

Go to `Kernel → Restart & Run All`

---

## 📁 Project Structure

```
uber-data-analysis-nyc/
│
├── uber_analysis_austin_mathew.ipynb    ← Main analysis notebook
│
├── uber-raw-data-janjune-15_sample.csv  ← Jan–Jun 2015 (sample)
├── uber-raw-data-apr14.csv
├── uber-raw-data-may14.csv
├── uber-raw-data-jun14.csv
├── uber-raw-data-jul14.csv
├── uber-raw-data-aug14.csv
├── uber-raw-data-sep14.csv
├── Uber-Jan-Feb-FOIL.csv                ← Dispatch base vehicle data
│
└── README.md
```

---


Made by **Austin Mathew**
