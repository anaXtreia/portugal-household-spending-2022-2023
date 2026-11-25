# Household spending in Portugal (2022–2023)

English · [Português](README.pt.md)

How do households in Portugal spend their money, and how does spending vary by region and income? This project analyses average annual expenditure per household using the [2022/2023 Household Budget Survey from Statistics Portugal (INE)](https://ine.pt/xurl/pub/439486878).

## Key findings

- Housing (39.3%), food (12.9%) and transport (12.1%) account for 64.3% of average household expenditure nationwide.
- Housing accounts for 39.3% of expenditure using households’ own rental estimates, 34.1% using INE’s model-based imputed rents, and 16.4% when households’ rental estimates are subtracted from both housing and total expenditure.
- Food accounts for a smaller share of spending in the highest income quintile than in the lowest (9.8% versus 15.8%), even though average annual food spending is higher (€3,442 versus €2,571).

## Reproduce the analysis

The notebooks are written in Portuguese. The analysis was verified with Python 3.13 and SQLite 3.50. The housing query requires SQLite 3.30 or later through Python’s built-in `sqlite3` module.

On macOS or Linux, run the following from the repository root.

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install jupyterlab numpy pandas matplotlib openpyxl
cd notebooks
jupyter lab
```

Run all cells in each notebook in the order below, with `notebooks/` as the kernel’s working directory.

1. [Data cleaning and preparation](notebooks/01_limpeza_idef.ipynb) reads the original Excel file and produces two CSV files in [`data/processed/`](data/processed/).
2. [Exploratory analysis](notebooks/02_analise_exploratoria.ipynb) reads the CSV files and compares spending across regions and income quintiles, including three housing scenarios.
3. [SQL analysis](notebooks/03_analise_sql.ipynb) loads the same CSV files into an in-memory SQLite database and answers four questions about household spending.

The processed CSV files are included in the repository. To explore the results with these files, start with the second or third notebook.

## Data and interpretation

- The [INE workbook](data/IDF20222023_a.xlsx) reports expenditure in euros and as a share of total expenditure by region (tables Q.2.1.a and Q.2.1.b) and income quintile (tables Q.2.11.a and Q.2.11.b).
- Housing and total expenditure under model-based imputation come from the table on owner-occupied housing valuation on page 36 of the INE publication. The scenario that excludes households’ rental estimates retains other non-monetary expenditure.
- Quintiles are based on 2021 equivalised income, and regions follow the 2013 NUTS II boundaries. Expenditure shares are ratios of group averages. Small regional differences should be interpreted with caution.
- Education expenditure for Alentejo is unavailable. Data cleaning preserves missing values and flags estimates identified by INE as having low reliability.
