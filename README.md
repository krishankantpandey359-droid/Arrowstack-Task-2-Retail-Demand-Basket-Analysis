# Retail Demand & Basket Analysis

**Author:** Srishti Pandey  
**Tools:** Python, Pandas, NumPy, Matplotlib, Google Colab  
**Dataset:** UCI Online Retail

## Project Overview

In this project, I analysed historical online retail transactions to understand sales patterns, identify important products and countries, and find products that often appear together in the same invoice. I also documented the data-cleaning decisions and checked the results before drawing conclusions.

The analysis uses transaction data from one online retailer. The results describe patterns in this dataset and should not be treated as proof of customer behaviour in every store or as a guarantee of future demand.

## Objectives

- Check the quality of the raw transaction data.
- Clean invalid and duplicate transaction records while keeping a record of the decisions.
- Explore monthly sales value, product performance and country contribution.
- Analyse product combinations in UK invoices using support, confidence and lift.
- Turn the findings into practical recommendations and state the limitations clearly.

## Dataset

The project uses the **Online Retail** dataset from the UCI Machine Learning Repository. The original dataset contains **541,909 transaction rows** and eight columns, including invoice number, product code, description, quantity, invoice date, unit price, customer ID and country.

- **Dataset page:** https://archive.ics.uci.edu/dataset/352/online%2Bretail
- **DOI:** https://doi.org/10.24432/C5BW33
- **License:** CC BY 4.0

Download the official `Online Retail.xlsx` file from the UCI dataset page before running the notebook in Google Colab.

## Data Cleaning

The notebook checks missing values, exact duplicate rows, cancellation invoices, invalid dates and non-positive quantities or prices. It creates a cleaned copy so that the original data remains available for checking.

After cleaning, **524,878 rows** remained for the main analysis. Rows with a missing `CustomerID` were kept when the invoice and product details were usable, because invoice-level analysis does not always require a customer ID. Large values were reviewed as potential outliers rather than automatically removed, since some may represent genuine large orders.

The sales summaries use positive transaction lines. They are not presented as final net revenue or profit because returns and operating costs are not fully accounted for.

## Analysis Performed

### 1. Monthly Sales Value

The notebook groups positive transaction-line sales value by month and visualises the pattern over time. In this run, **November 2011** had the highest monthly positive-line sales value at **£1,503,866.78**.

### 2. Product Analysis

Products are compared using sales value, units sold and invoice frequency. In this run, **REGENCY CAKESTAND 3 TIER** had the highest positive-line sales value in the cleaned data at **£174,156.54**.

### 3. Country Analysis

The notebook compares country-level sales value, invoice counts and units sold. The **United Kingdom** had the highest positive-line sales value at **£9,001,744.09**.

### 4. Market Basket Analysis

The basket analysis focuses on UK invoices and the 25 most frequently invoiced products. Postage lines are excluded from baskets because postage is a service charge rather than a merchandise item.

- UK invoice baskets analysed: **17,979**
- Products included in the basket matrix: **25**
- Directional candidate rules calculated: **600**
- Rules meeting the selected thresholds: **344**

The selected thresholds were minimum support of 0.003, minimum confidence of 0.15 and lift greater than 1. In this run, the highest-lift rule among the qualifying rules was **LUNCH BAG CARS BLUE → LUNCH BAG PINK POLKADOT**, with support **2.614%**, confidence **44.1%** and lift **7.89**.

Support measures how often a pair appears across all baskets, confidence measures how often the consequent appears when the antecedent is present, and lift compares the observed association with what would be expected if the items were independent. These measures show association, not causation.

## Main Findings

- November 2011 had the highest monthly positive-line sales value in this dataset.
- REGENCY CAKESTAND 3 TIER was the top product by positive-line sales value in the cleaned data.
- The United Kingdom contributed the largest positive-line sales value.
- Some lunch-bag designs appeared together more often than expected under independence in the selected UK basket analysis.

## Recommendations

- Test a small number of strong product associations as bundles or cross-selling suggestions, then compare the results with normal sales.
- Use monthly patterns and product rankings as inputs to stock monitoring, alongside current inventory and supplier lead times.
- Study repeat purchases using records with available customer IDs.
- Repeat the analysis on newer data to see whether the patterns continue.
- Measure the effect of any bundle or stock-planning change before making it a wider business decision.

## Limitations

- The dataset covers about one year from one retailer, so the results may not generalise to other retailers or later periods.
- Positive transaction-line sales value is not the same as net revenue or profit.
- Missing customer IDs limit customer-level analysis.
- Basket analysis covers UK invoices and only the 25 most frequently invoiced products, so less common product combinations may be missed.
- Products appearing in the same invoice do not necessarily cause one another to be purchased.

## How to Run

1. Download `Online Retail.xlsx` from the official UCI dataset page.
2. Open the notebook in Google Colab.
3. Run the dataset-loading cell and upload `Online Retail.xlsx` when prompted.
4. Run the cells from top to bottom.
5. Check that the tables and plots appear and that the final validation cell prints:

   `PASS: All final validation checks passed.`

The notebook includes data-quality checks and validation assertions to help confirm that the main analysis steps have completed.

## Project Files

- `Task_2_Retail_Demand_Basket_Analysis_Srishti_Pandey.ipynb` — analysis notebook
- `Retail_Demand_Basket_Analysis_Srishti_Pandey.pptx` — project presentation
- `README.md` — project overview, methods, findings and instructions

## Data Acknowledgement

Chen, D. (2015). *Online Retail*. UCI Machine Learning Repository. https://doi.org/10.24432/C5BW33

Retail demand analysis and market basket analysis using Python, Pandas and association rules.
