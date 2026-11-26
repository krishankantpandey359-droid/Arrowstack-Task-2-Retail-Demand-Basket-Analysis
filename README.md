# Retail Demand & Basket Analysis

A reproducible Python analysis of the UCI Online Retail transactions. The project examines sales patterns, product performance, country contribution and product associations within UK invoices.

**Author:** Srishti Pandey  
**Stack:** Python, Pandas, NumPy, Matplotlib, Jupyter and Google Colab  
**Dataset:** UCI Online Retail, 541,909 source transaction lines

## Business questions

1. How does positive transaction-line value change month by month?
2. Which merchandise items lead by value, units and invoice frequency?
3. Which countries contribute the largest positive transaction-line value?
4. Which products frequently appear together in UK invoices?

## Repository contents

| File | Purpose |
|---|---|
| `Task_2_Retail_Demand_Basket_Analysis_Srishti_Pandey (2).ipynb` | Canonical end-to-end analysis, cleaning log, visualisations and validation |
| `DATA_DICTIONARY.md` | Source fields, derived measures and interpretation rules |
| `requirements.txt` | Bounded Python dependencies |
| `.github/workflows/project-checks.yml` | Automated notebook execution and validation |
| `Task_2_Retail_Demand_Basket_Analysis_Srishti_Pandey_ppt.pptx` | Project presentation |

## Setup

Python 3.11 is recommended.

```bash
git clone https://github.com/krishankantpandey359-droid/Arrowstack-Task-2-Retail-Demand-Basket-Analysis.git
cd Arrowstack-Task-2-Retail-Demand-Basket-Analysis
python -m venv .venv
```

Activate the environment, then install dependencies:

```bash
# Windows
.venv\\Scripts\\activate

# macOS / Linux
source .venv/bin/activate

python -m pip install -r requirements.txt
```

Download the official `Online Retail.xlsx` workbook from the [UCI dataset page](https://archive.ics.uci.edu/dataset/352/online+retail) and place it in the repository root. In Google Colab, open the canonical notebook and upload the workbook when prompted. Run all cells from top to bottom.

## Data preparation

The notebook keeps the raw DataFrame unchanged and creates a separate working copy. It reports source exceptions before cleaning, including exact duplicates, cancellation invoices, invalid or non-finite numeric values, non-positive quantities and prices, and missing customer identifiers. A sequential cleaning log reports row counts before and after each step.

Missing `CustomerID` values are retained when the invoice and product fields needed for invoice-level analysis are valid. Large values are flagged for review rather than automatically removed. Invoice dates are parsed with Pandas' default month-first interpretation for the source workbook, then checked to remain within the 2010–2011 source period.

## Analysis and interpretation

- Monthly and country summaries use positive transaction lines.
- Merchandise rankings exclude postage and manual-entry descriptions.
- Basket analysis uses UK invoices and the 25 most frequently invoiced products.
- Association rules report support, confidence and lift. Threshold sensitivity is also examined.

The measure `Quantity × UnitPrice` is a transaction-line value. It is not profit, gross margin or net revenue after returns and costs. Positive associations do not establish that one product causes another to be purchased.

## Observed findings in the committed notebook output

- Cleaned transaction rows: 524,878.
- UK invoice baskets analysed: 17,979.
- Products in the basket matrix: 25.
- Directional candidate rules: 600.
- Rules meeting the selected thresholds: 344.
- November 2011 has the highest positive-line sales value in the saved analysis output: £1,503,866.78.
- The United Kingdom has the highest positive-line sales value in the saved analysis output: £9,001,744.09.

These figures describe the committed notebook output. Re-run the notebook against the official workbook to reproduce them. They are descriptive results, not forecasts or causal evidence.

## Reproducibility and validation

The GitHub Actions workflow downloads the official UCI workbook, executes the canonical notebook from top to bottom, checks that all non-empty code cells ran without errors, and confirms that the final validation cell printed its PASS message. The notebook also validates required fields, positive and finite transaction values, cleaning-log consistency, summary outputs, basket dimensions and association-rule thresholds.

Run the same end-to-end check locally with:

```bash
jupyter nbconvert --to notebook --execute "Task_2_Retail_Demand_Basket_Analysis_Srishti_Pandey (2).ipynb" --output executed_retail.ipynb --ExecutePreprocessor.timeout=1200
```

## Data source and attribution

Chen, D. (2015). *Online Retail*. UCI Machine Learning Repository. [https://doi.org/10.24432/C5BW33](https://doi.org/10.24432/C5BW33). Dataset page: [UCI Online Retail](https://archive.ics.uci.edu/dataset/352/online+retail). License: CC BY 4.0.

## Limitations

- The dataset represents one retailer over a limited historical period.
- Positive transaction-line sales value is not net revenue or profit.
- Missing customer IDs limit customer-level analysis.
- Basket analysis covers UK invoices and only the 25 most frequently invoiced products.
- Products appearing in the same invoice do not necessarily cause one another to be purchased.
- Validate findings on newer data and through controlled business tests before operational use.

## Latest GitHub Actions validation

Latest verified successful main-branch workflow run checked on 24 November 2026: [GitHub Actions run #45313979613](https://github.com/krishankantpandey359-droid/Arrowstack-Task-2-Retail-Demand-Basket-Analysis/actions/runs/45313979613). This run verifies the checks configured in this repository's workflow; it does not replace manual testing of features outside CI.
