## Data

This project uses the [Yelp Open Dataset](https://business.yelp.com/data/resources/open-dataset/),
filtered to the *Coffee & Tea* category. Yelp provides the dataset for non-commercial,
educational use and does not permit redistribution, so **no Yelp data is included in this
repository.**

The analysis runs against three tables built in Databricks — `coffee_reviews` (~442K rows),
`coffee_shops` (~6.7K), and `coffee_users` (~259K) produced by a two-stage pipeline:

1. **Stage 1 (Google Colab):** stream-load the raw `business.json`, `review.json`, and
   `user.json`, filter to the Coffee & Tea category, and write Parquet.
2. **Stage 2 (Databricks):** load the Parquet into Delta tables and run the SQL / PySpark / NLP
   analysis in `coffeeking_yelp_analysis.ipynb`.

**To reproduce:** request the dataset directly from Yelp, then run Stage 1 followed by Stage 2.
Raw review and user records have been cleared from the committed notebook outputs to respect the
dataset terms.

*Independent analysis — not affiliated with, sponsored by, or endorsed by Yelp.*
