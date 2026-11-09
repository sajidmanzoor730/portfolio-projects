# NYC 311 Service Requests: Data Quality and Service Performance

This project was transferred from the live portfolio source repository. It uses the official NYC Open Data 311 Service Requests dataset (Socrata ID `erm2-nwe9`).

## Provenance

The portfolio's source README records a successful GitHub Actions live-data run for 1–31 July 2026 (end date exclusive): 343,133 records, zero duplicate unique keys, zero missing/unparseable creation timestamps, 74 closure-before-creation anomalies blanked during cleaning, and 460 unspecified/blank borough values.

The checked-in result CSVs are the result tables from that source project. Treat them as a dated extract, not permanent current totals. Re-run the workflow to refresh. The full raw extract is not included here.

## Run

```bash
python -m pip install -r requirements.txt
python download_311.py --start 2026-07-01 --end 2026-08-01
python quality_checks.py
python clean_311.py
python run_analysis.py
```

The end date is exclusive. Add `--app-token YOUR_TOKEN` to the downloader if the public API throttles requests.

## Contents

- Download script for the official NYC Open Data API.
- Raw-data quality checks and documented cleaning rules.
- SQLite SQL analysis queries.
- Python runner that exports named result tables.
- Dashboard design notes.
- Result CSVs from the portfolio source.
- A stand-in data generator for local dry runs only.

## Interpretation limits

- The public source is updated daily; a later extract can differ.
- Recorded elapsed time is not automatically an official SLA.
- Open requests have censored closure duration; do not treat them as zero.
- Repeat address/problem combinations are indicators for investigation, not proof of a persistent issue.
- Stand-in test data is synthetic and must never be reported as real findings.

Official source: https://data.cityofnewyork.us/Social-Services/311-Service-Requests-from-2020-to-Present/erm2-nwe9
