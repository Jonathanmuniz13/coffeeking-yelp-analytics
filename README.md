# CoffeeKing: Yelp Coffee-Shop Analytics at Scale

![Spark](https://img.shields.io/badge/Apache%20Spark-SQL%20%2B%20PySpark-E25A1C?logo=apachespark&logoColor=white)
![Databricks](https://img.shields.io/badge/platform-Databricks-FF3621?logo=databricks&logoColor=white)
![NLP](https://img.shields.io/badge/NLP-TF--IDF%20%2B%20word%20clouds-1F7A63)
![Status](https://img.shields.io/badge/status-complete-success)

A **Spark/Databricks** pipeline over **~442K Yelp reviews** (6.7K coffee & tea shops, 259K users) that turns raw review data into location, hours, and service recommendations for a coffee startup — ending in a stakeholder deck of prioritized actions.

📊 **[Read the full project write-up →](https://jonathanmuniz13.github.io/PORTFOLIO-REPO/projects/coffeeking/)**
📑 **[View the stakeholder deck →](https://docs.google.com/presentation/d/e/2PACX-1vQ2gc_SUFx9DOQhVTEV_O6wOZNtwTZ88puy1h4RHcJ74mXOzl79MKs3s2L8RtxPMfgO8bbm1004bpx1/pub)**

---

## Three questions, answered

1. **When to open** — top-rated shops (≥4.5★) cluster in **7 AM–5 PM** windows, peaking weekend mornings
2. **Where to open** — a ZIP-level cut for **≥20 shops but ≤3.5★** surfaced high-density, low-satisfaction markets (Tampa, Reno, suburban Philadelphia) ripe for disruption
3. **What drives ratings** — NLP on a balanced 1★/5★ sample shows five-star language is about **product & people**, one-star language about **process failures** (slow/incorrect service) — so service speed is the highest-leverage fix

A correlation study added a useful null: ZIP-level shop density barely relates to average rating (r ≈ 0.19) — saturation doesn't predict quality, execution does.

## Pipeline

Two stages, keeping the heavy lifting off the cluster:

1. **Google Colab** — stream-load multi-GB `business.json` / `review.json` / `user.json`, filter to *Coffee & Tea*, explode nested business-hours, write Parquet shards
2. **Databricks** — load shards as Delta tables, analyze in **Spark SQL + Python** (matplotlib/seaborn/folium/wordcloud), including ZIP rollups, reusable temp views, and handling ~1,300 shops with placeholder/missing hours

## ⚠️ Data — not included in this repo

This project uses the **Yelp Open Dataset**, which is **not committed** here (size + license terms — the dataset is for non-commercial academic use and prohibits redistribution).

1. Request the dataset from [yelp.com/dataset](https://www.yelp.com/dataset).
2. Run the Colab cleaning stage to produce the Parquet shards.
3. Load the shards into Databricks as Delta tables, then run the notebook.

## Repository structure

```
.
├── CoffeeKing_Yelp_Review_Study.ipynb   # Databricks notebook (Spark SQL + Python)
├── colab_cleaning.ipynb                 # Stage 1: JSON → Parquet
├── .gitignore                           # excludes raw JSON / Parquet
└── README.md
```

## How to run

The analysis runs on **Databricks** (Spark SQL + PySpark). Import `CoffeeKing_Yelp_Review_Study.ipynb` into a Databricks workspace, attach a cluster, and run after loading the Delta tables (see Data above). The Colab stage runs in any standard Python environment with `pandas` / `pyarrow`.

## Tools

`Apache Spark` · `Spark SQL` · `PySpark` · `Databricks` · `Delta Lake` · `Python` · `NLTK` · `folium`

## Author

**Jonathan Muniz** — [Portfolio](https://github.com/Jonathanmuniz13/coffeeking-yelp-analytics) · [LinkedIn](https://www.linkedin.com/in/jonathan-muniz-fl) · [GitHub](https://github.com/Jonathanmuniz13)

*Coursera SQL for Data Science capstone, extended onto a Spark/Databricks stack.*
