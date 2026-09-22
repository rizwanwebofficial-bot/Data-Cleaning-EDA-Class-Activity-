# Airbnb NYC — Data Cleaning & EDA (Class Activity)

A guided data-cleaning and exploratory data analysis (EDA) exercise on the NYC Airbnb listings dataset, done as a class activity for **AI & ML Launchpad, Cohort 1**, taught by [**Abdul Wahab**](https://github.com/Wahab901278).

> [!NOTE]
> **Work in progress.** The activity is a set of 48 guided questions; this notebook currently covers **30 of them**. The remaining questions (further visualization, outlier handling, and feature preparation for machine learning) are not yet done. This README will be updated as more questions are completed.

---

## About the Dataset

`Airbnb.csv` — **48,900 rows, 16 columns** of NYC Airbnb listing data: `id`, `name`, `host_id`, `host_name`, `neighbourhood group`, `neighbourhood`, `latitude`, `longitude`, `room type`, `price`, `minimum nights`, `number_of_reviews`, `last review`, `reviews_per_month`, `calculated_host_listings_count`, `availability_365`.

At load time, four columns have missing values: `name` (16), `host_name` (21), `last review` (10,052) and `reviews_per_month` (10,052) — the last two are missing together, since a listing with no review date naturally has no reviews-per-month figure either.

---

## What the Notebook Covers So Far

Organized in the order the notebook follows:

**1. Setup and first look**
- Import pandas, numpy, matplotlib, seaborn and `missingno`
- Load the CSV, inspect with `head()` / `tail()` / `shape`
- Standardize column names (spaces → underscores)
- Check data types with `df.info()`

**2. Cleaning**
- Convert `price` and `minimum_nights` from float to integer
- Identify and remove exact duplicate rows
- Visualize missing-value patterns with `missingno` (matrix and heatmap)
- Confirm that rows with `number_of_reviews == 0` are exactly the rows missing `reviews_per_month` and `last_review`
- Impute `reviews_per_month` with 0 for listings with zero reviews; fill missing `name`/`host_name` with placeholder labels; deliberately leave `last_review` as a true missing value rather than inventing a date

**3. Feature extraction**
- Replace the `id` column with a rank-based feature (lower rank ≈ older listing), and drop identifier columns that don't add analytical value
- Find and fix a typo in `neighbourhood_group` ("Broklyn" → "Brooklyn"), catching a 6th, invalid borough value in what should only ever be NYC's 5 boroughs

**4. Analysis questions**
- Top 10 hosts by number of bookings (by host ID, and separately by host name — with a note on why host name is not a safe grouping key, since multiple hosts share a name)
- Room type of the top-booked host
- How listing supply splits across room types, and how that split differs by borough
- Which neighbourhood group has the highest number of bookings (and why a pie chart was rejected as the visualization for this)
- Summary statistics for `price`, including a check on why the average and standard deviation differ so much (an early signal of skew/outliers)
- Minimum and maximum listing prices, flagging $0/night listings as a likely data quality issue
- Average and median price by room type
- Total reviews by neighbourhood group
- Set/reset index practice on the `price` column
- A pivot table of median price by borough × room type, with a note on why the "All" margin isn't a simple average of the borough medians (median is a positional statistic, not additive)

Each analysis step is followed by a short written interpretation in the notebook, not just code output.

---

## Not Done Yet

- The remaining ~18 of the 48 guided questions
- Outlier handling for `price` (the $0 listings and the long right tail noted above are flagged but not yet treated)
- Visualization beyond the missingno plots and the pivot table (distribution plots, borough-level comparisons)
- Preparing the cleaned data for a machine learning model (encoding, scaling, train/test split), which is the stated end goal of the activity

---

## Tech Stack

pandas, numpy, matplotlib, seaborn, missingno — in a Jupyter notebook.

## How to Run

```bash
pip install pandas numpy matplotlib seaborn missingno jupyter
jupyter notebook airbnb.ipynb
```

Keep `Airbnb.csv` in the same folder as the notebook — it's loaded by relative path.

---

## Credits

Class: **AI & ML Launchpad, Cohort 1**
Instructor: [Abdul Wahab](https://github.com/Wahab901278)
