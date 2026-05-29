Uber Data Analysis — New York City (2014–2015)
📓 Notebook : uber_analysis_austin_mathew.ipynb
---
Problem Statement
This project analyses Uber pickup data across New York City to uncover demand patterns at both a macro and micro level. The goal is to answer key operational and behavioural questions: When does demand peak? Where does demand concentrate? Which dispatch bases drive the majority of trips? And how does airport-specific demand behave across the day?
By identifying these patterns, ride-hailing operators and city planners can optimise driver allocation, reduce wait times, and anticipate surge demand by time, location, and day of week.
---
Datasets Used
File	Description
`uber-raw-data-janjune-15_sample.csv`	~1M sampled pickups from Jan–Jun 2015 (sample of 15M row full dataset)
`uber-raw-data-apr14.csv` … `uber-raw-data-sep14.csv`	Monthly raw pickup data, Jul–Sep 2014
`Uber-Jan-Feb-FOIL.csv`	FOIL-requested data with active vehicle counts per dispatching base
---
Steps Followed
Step 1 : Loaded the Jan–Jun 2015 sample dataset into a Pandas DataFrame.
Step 2 : Performed data quality checks — identified and removed duplicate rows (verified via `.duplicated().sum()`), confirmed no missing values except in derived columns.
Step 3 : Converted the `Pickup_date` column from `object` dtype to `datetime64` using `pd.to_datetime()`.
Step 4 : Extracted derived time features — `month`, `weekday`, `day`, `hour`, and `minute` — from the datetime column for time-series and categorical analysis.
Step 5 : Built a cross-tab pivot table (`pd.crosstab`) of pickups by Month × Weekday and visualised it as a grouped bar chart using Plotly Express.
Step 6 : Analysed hourly rush patterns by weekday using a `groupby` on `['weekday', 'hour']`, with a Categorical sort to maintain correct weekday order, then plotted as a multi-line chart.
Step 7 : Performed a Pareto Analysis on dispatching base numbers to identify which bases account for 80% of all trips, using a dual-axis bar + cumulative line chart (`plotly.graph_objs`).
Step 8 : Conducted Airport Demand Analysis — filtered pickups by LocationIDs for EWR, JFK, and LGA, then charted hourly pickup volume per airport using a Plotly area chart.
Step 9 : Combined the six monthly 2014 raw files programmatically using `os.listdir()` + `pd.concat()` into a unified `final` DataFrame, removing duplicates post-merge.
Step 10 : Identified geographic rush hotspots across NYC using `folium.HeatMap` and `HeatMapWithTime` (animated hourly heatmap) on a CartoDB basemap.
Step 11 : Built a Day × Hour pivot heatmap using `.groupby(['day','hour']).size().unstack()` with Pandas `.style.background_gradient()` for at-a-glance rush pattern identification.
Step 12 : Wrapped the pivot heatmap logic into a reusable `gen_pivot_table(df, col1, col2)` function to automate pairwise analysis across any two categorical/time columns.
---
Visualisations
📊 Grouped Bar Chart — Monthly pickups broken down by weekday
📈 Multi-Line Chart — Hourly pickup demand by day of week (24-hour view)
📉 Pareto Chart — Dispatching base trip share with 80% threshold line
🗺️ Area Chart — Hourly airport demand pressure (EWR vs JFK vs LGA)
🔥 Folium Static Heatmap — Geographic density of all pickups across NYC
🌊 Folium HeatMapWithTime — Animated hourly heatmap showing rush movement
🎨 Gradient Pivot Table — Day × Hour pickup matrix with background gradient styling
🎻 Box & Violin Plots — Active vehicle distribution per dispatching base
---
Key Insights
[1] Monthly & Weekly Demand
June records the highest number of Uber pickups among the Jan–Jun 2015 sample.
Friday and Saturday consistently show the highest daily demand across all months, suggesting weekend leisure and nightlife activity drive a significant share of rides.
[2] Hourly Rush Patterns
Saturday and Sunday show similar demand trends through the morning but diverge in the evening — Saturday demand keeps climbing late into the night, while Sunday tapers off after the early evening.
Thursday nights exhibit demand trends almost identical to Friday and Saturday, suggesting New Yorkers begin their effective weekend on Thursday.
[3] Dispatching Base (Pareto)
A small number of dispatch bases account for ~80% of all Uber trips, confirming the Pareto principle applies to ride-hailing base distribution.
[4] Airport Demand
JFK and LGA dominate airport pickup volumes. Demand at all three airports spikes in the early morning and again during the evening rush, consistent with major flight departure/arrival windows.
[5] Geographic Hotspots
Midtown Manhattan is the single brightest hotspot on the heatmap.
High-density zones extend from Midtown down to Lower Manhattan, with secondary clusters in Upper Manhattan and the Heights of Brooklyn.
---
Tech Stack
Tool	Purpose
Python 3	Core language
Pandas	Data loading, cleaning, feature engineering, pivot tables
NumPy	Numerical operations
Plotly Express	Bar, line, area charts
Plotly Graph Objects	Pareto (dual-axis) chart
Folium	Geographic heatmaps (static + animated)
Seaborn / Matplotlib	Supplementary plotting
Jupyter Notebook	Interactive development environment
---
How to Run
Clone this repository and navigate to the project folder.
Place all dataset CSV files in the same directory as the notebook (or update the `DATA_PATH` variable in the first cell).
Install dependencies:
```bash
   pip install pandas numpy plotly folium seaborn matplotlib
   ```
Open the notebook:
```bash
   jupyter notebook uber_analysis_austin_mathew.ipynb
   ```
Run all cells top-to-bottom (`Kernel → Restart & Run All`).
> **Note:** The full `uber-raw-data-janjune-15.csv` file is ~15M rows. The sample version (`_sample.csv`) with ~1M rows is recommended unless you have sufficient RAM.
---
Project Structure
```
├── uber_analysis_austin_mathew.ipynb   # Main analysis notebook
├── uber-raw-data-janjune-15_sample.csv # Jan–Jun 2015 sample data
├── uber-raw-data-apr14.csv             # Apr 2014 raw data
├── uber-raw-data-may14.csv             # May 2014 raw data
├── uber-raw-data-jun14.csv             # Jun 2014 raw data
├── uber-raw-data-jul14.csv             # Jul 2014 raw data
├── uber-raw-data-aug14.csv             # Aug 2014 raw data
├── uber-raw-data-sep14.csv             # Sep 2014 raw data
├── Uber-Jan-Feb-FOIL.csv               # Active vehicle FOIL data
└── README.md
```
---
Analysis by Austin Mathew
