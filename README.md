# Retail Demand & Basket Analysis

A reproducible Python analysis of the UCI Online Retail transactions. The project examines sales patterns, product performance, country contribution and product associations within UK invoices.

**Author:** Srishti Pandey  
**Stack:** Python, Pandas, NumPy, Matplotlib, Jupyter  
**Dataset:** UCI Online Retail, 541,909 source transaction lines

## Business questions

1. How does positive transaction-line value change month by month?
2. Which merchandise items lead by value, units and invoice frequency?
3. Which countries contribute the largest positive transaction-line value?
4. Which products frequently appear together in UK invoices?

## Repository contents

| File | Purpose |
|---|---|
| `retail_demand_basket_analysis.ipynb` | End-to-end analysis, cleaning log, visualisations and validation |
| `DATA_DICTIONARY.md` | Source fields, derived measures and interpretation rules |
| `requirements.txt` | Reproducible Python dependencies |
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

Download the official `Online Retail.xlsx` workbook from the [UCI dataset page](https://archive.ics.uci.edu/dataset/352/online+retail) and place it in the repository root. Open `retail_demand_basket_analysis.ipynb` in Jupyter or upload the workbook when prompted in Google Colab.

Run the notebook from top to bottom. The final cell prints a PASS message when the data-quality and output assertions succeed.

## Data preparation

The notebook keeps the raw DataFrame unchanged and creates a separate working copy. It reports source exceptions before cleaning, including duplicate rows, cancellation invoices, invalid or non-finite numeric values, non-positive quantities and prices, and missing customer identifiers.

Missing `CustomerID` values are retained when the invoice and product fields needed for invoice-level analysis are valid. Large values are flagged for review rather than automatically removed. A sequential cleaning log reports the row count before and after each cleaning step.

## Analysis and interpretation

- Monthly and country summaries use positive transaction lines.
- Merchandise rankings exclude postage and manual-entry descriptions.
- Basket analysis uses UK invoices and the 25 most frequently invoiced products.
- Association rules report support, confidence and lift. Threshold sensitivity is also examined.

The measure `Quantity × UnitPrice` is a transaction-line value. It is not profit, gross margin or net revenue after returns and costs. Positive associations do not establish that one product causes another to be purchased.

## Data source and attribution

Chen, D. (2015). *Online Retail*. UCI Machine Learning Repository. [https://doi.org/10.24432/C5BW33](https://doi.org/10.24432/C5BW33).

Dataset page: [UCI Online Retail](https://archive.ics.uci.edu/dataset/352/online+retail).  
License: CC BY 4.0.

## Limitations

The dataset represents one retailer over a limited historical period. Basket analysis is restricted to UK invoices and the 25 most frequently invoiced products. Missing customer IDs limit customer-level analysis. The findings are descriptive and should be validated on newer data and through controlled business tests before operational decisions are made.
