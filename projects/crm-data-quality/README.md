# CRM Data Quality & Cleanup

A reproducible record-level cleanup workflow based on the CRM project published in Sajid Manzoor's portfolio.

## Dataset and provenance

- Synthetic dataset covering January–September 2026.
- Raw file: 3,090 rows.
- The published clean dataset contains 3,000 records; the portfolio describes 90 duplicate records merged/removed.
- Email addresses use the reserved `.example` domain. These are not real customer, employer, or contact records.
- No real customer data is included.

## Files

- `data/CRM_Data_Quality_Dataset_Raw.csv`: original synthetic input.
- `data/CRM_Data_Quality_Dataset_Clean.csv`: published cleaned output.
- `scripts/clean_crm.py`: deterministic cleanup workflow.

## Run

From this project directory:

```bash
python -m pip install pandas
python scripts/clean_crm.py
```

The script writes `output/crm_cleaned.csv` and prints row counts, duplicate removals, invalid emails, follow-up flags, and a comparison against the published clean file.

## Cleanup rules

1. Trim and normalize company-name casing and whitespace.
2. Normalize US/Canada and UK phone formats.
3. Normalize email casing and common punctuation errors; blank and flag addresses that remain invalid.
4. Keep the earliest Record_ID when a later row repeats an email or normalized company name.
5. Flag missing email, phone, or industry for owner follow-up; do not guess missing values.

## Important implementation note

The script intentionally does not perform external enrichment. It compares its deterministic result with the published clean dataset; any remaining differences are documented as values present in the published output but not inferred by the rule-based cleaner.
