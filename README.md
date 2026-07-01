# CoffeeKing: Yelp Coffee-Shop Analytics at Scale

![Spark](https://img.shields.io/badge/Apache%20Spark-SQL%20%2B%20PySpark-E25A1C?logo=apachespark&logoColor=white)
![Databricks](https://img.shields.io/badge/platform-Databricks-FF3621?logo=databricks&logoColor=white)
![NLP](https://img.shields.io/badge/NLP-TF--IDF%20%2B%20word%20clouds-1F7A63)
![Status](https://img.shields.io/badge/status-complete-success)

A Spark/Databricks pipeline over roughly 442K Yelp reviews (6.7K coffee and tea shops, 259K users) that turns raw review data into location, hours, and service recommendations for a coffee startup, ending in a stakeholder deck of prioritized actions.

馃搳 **[Read the full project write-up 鈫抅(https://jonathanmuniz13.github.io/PORTFOLIO-REPO/projects/coffeeking/)**
馃搼 **[View the stakeholder deck 鈫抅(https://docs.google.com/presentation/d/e/2PACX-1vQ2gc_SUFx9DOQhVTEV_O6wOZNtwTZ88puy1h4RHcJ74mXOzl79MKs3s2L8RtxPMfgO8bbm1004bpx1/pub)**

---

## Three questions, answered

1. **When to open.** Top-rated shops (4.5 stars and up) cluster in 7 AM to 5 PM windows, peaking on weekend mornings.
2. **Where to open.** A ZIP-level cut for 20 or more shops averaging 3.5 stars or below surfaces twelve saturated, low-satisfaction markets, led by Tampa (33607, 33612, 33511, 33578), Philadelphia (19102, 19406, 18901), and Nashville (37214, 37211), plus Tucson (85719), Reno (89503), and the Indianapolis suburbs (46038). Loosening the bar to 10 or more shops widens the field to roughly 95 ZIPs.
3. **What drives ratings.** NLP on a balanced sample of 1 star and 5 star reviews shows five-star language centers on product and people, while one-star language centers on process failures like slow or incorrect service, making service speed the highest-leverage fix.

A correlation study added a useful null result: ZIP-level shop density barely relates to average rating (r ~ 0.19). Saturation does not predict quality; execution does.

<!-- REVIEWER ENGAGEMENT (optional): confirm the correct top-reviewer count before
     adding. Draft once confirmed, e.g.:
     "Reviewer engagement follows a steep power law: the single most active
      reviewer posted [NNN] reviews, far above the median." -->

## Pipeline

Two stages, keeping the heavy lifting off the cluster:

1. **Google Colab.** Stream-load multi-GB business.json, review.json, and user.json, filter to the Coffee and Tea category, explode nested business hours, and write Parquet shards.
2. **Databricks.** Load the shards as Delta tables and analyze in Spark SQL and Python (matplotlib, seaborn, folium, wordcloud), including ZIP rollups, reusable temp views, and handling roughly 1,300 shops with placeholder or missing hours.

## Data is not included in this repo

This project uses the **Yelp Open Dataset**, which is not committed here (size plus license terms; the dataset is for non-commercial academic use and prohibits redistribution).

1. Request the dataset from [yelp.com/dataset](https://www.yelp.com/dataset).
2. Run the Colab cleaning stage to produce the Parquet shards.
3. Load the shards into Databricks as Delta tables, then run the notebook.

## Repository structure

```
.
|-- CoffeeKing_Yelp_Review_Study.ipynb   # Databricks notebook (Spark SQL + Python)
|-- colab_cleaning.ipynb                 # Stage 1: JSON to Parquet
|-- .gitignore                           # excludes raw JSON / Parquet
`-- README.md
```

## How to run

The analysis runs on **Databricks** (Spark SQL and PySpark). Import CoffeeKing_Yelp_Review_Study.ipynb into a Databricks workspace, attach a cluster, and run after loading the Delta tables (see Data above). The Colab stage runs in any standard Python environment with pandas and pyarrow.

## Tools

`Apache Spark` 路 `Spark SQL` 路 `PySpark` 路 `Databricks` 路 `Delta Lake` 路 `Python` 路 `NLTK` 路 `folium`

## Author

**Jonathan Muniz** 鈥?[Portfolio](https://jonathanmuniz13.github.io/PORTFOLIO-REPO/) 路 [LinkedIn](https://www.linkedin.com/in/jonathan-muniz-fl) 路 [GitHub](https://github.com/Jonathanmuniz13)

*Coursera SQL for Data Science capstone, extended onto a Spark/Databricks stack.*
