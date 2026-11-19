# Data Dictionary and Metric Definitions

## Source

The project uses the UCI Online Retail dataset (Chen, 2015), DOI: [10.24432/C5BW33](https://doi.org/10.24432/C5BW33). The source workbook contains 541,909 transaction lines from a UK-based online retailer. The dataset is distributed under CC BY 4.0. Obtain the workbook from the [official UCI dataset page](https://archive.ics.uci.edu/dataset/352/online+retail).

## Source fields

| Field | Meaning | Notes |
|---|---|---|
| InvoiceNo | Invoice identifier | Values beginning with `C` identify cancellations. |
| StockCode | Product identifier | Used to identify distinct products. |
| Description | Product description | Text label, not a unique key. |
| Quantity | Units on an invoice line | Negative values can represent returns. |
| InvoiceDate | Transaction date and time | Parsed as a datetime. |
| UnitPrice | Price per unit | Dataset currency is GBP (£). |
| CustomerID | Customer identifier | Missing values are retained for invoice-level analysis when other required fields are valid. |
| Country | Customer country | Used for geographic summaries. |

## Derived measures

- `LineValue`: `Quantity × UnitPrice` for a transaction line.
- Positive-line sales value: sum of `LineValue` after excluding cancellations and non-positive quantities/prices. This is not net revenue, gross margin, or profit.
- Invoice count: distinct `InvoiceNo` values in the relevant group.
- Basket support: proportion of eligible UK invoice baskets containing both items.
- Rule confidence: proportion of baskets containing the antecedent that also contain the consequent.
- Lift: confidence divided by the consequent's support. Lift above 1 indicates positive association in this sample, not causation.

## Interpretation rules

- Report returns and cancellations separately from positive-sale summaries where needed.
- Do not label transaction-line value as profit or net revenue.
- Keep postage and manual-entry lines out of merchandise rankings and basket rules, while documenting whether broader transaction summaries include them.
- Treat basket associations as hypotheses for controlled testing, not as causal evidence.
