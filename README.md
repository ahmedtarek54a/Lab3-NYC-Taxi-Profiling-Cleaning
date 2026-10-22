# Lab 3: NYC Taxi Data Profiling & Cleaning

**Course:** INF4058 Data Engineering  
**Dataset:** `yellow_tripdata_2021-01.csv.gz` (January 2021 Yellow Taxi trips)

## Scope
This project profiles the source in 100,000-row chunks, counts data-quality issues, and demonstrates a `clean(df)` function. It deliberately stops at cleaning and does **not** load cleaned data into PostgreSQL.

## Setup and run
Use Python 3.10+ in a virtual environment, then:

```bash
python -m pip install pandas
python lab3_nyc_taxi.py
```

The script downloads the dataset if it is not present. If network access is restricted, download the source from the URL below and place it next to the script.

Source: https://github.com/DataTalksClub/nyc-tlc-data/releases/download/yellow/yellow_tripdata_2021-01.csv.gz

## Outputs
The script prints the preview, dtypes, full-column profiling table, quality issue counts, and cleaning counts. It saves reproducible outputs under `outputs/`:
- `column_profile.csv`
- `data_quality_counts.csv`
- `profiling_summary.json`
- `cleaning_demo.json`

The cleaning rules required by the assignment are applied in order:
1. Remove rows where `passenger_count` is null.
2. Remove rows with invalid pickup timestamps or pickup timestamps outside January 2021.
3. Remove rows where `fare_amount <= 0`.

The `clean(df)` function copies the input and returns `(cleaned_df, removed_rows)`. Rule counts are sequential, so a row overlapping multiple rules is counted only once in the total removed rows.

Other detected issues (zero passenger count and non-positive trip distance) are profiled and reported, but not automatically removed by `clean(df)`, because the assignment's explicit cleaning rules name only the three rules above. Explain and justify that decision in your report.

## Important submission notes
- Do not commit the CSV/GZ data, `.venv/`, secrets, or credentials.
- Capture your own screenshots after running the script. Screenshots must show the command/output and your terminal prompt.
- Add your name, student ID, actual screenshots, observed error/fix (if any), and your GitHub URL to the report before submission.
- Never claim screenshots, class commands, Docker results, or error fixes that you did not personally observe.
