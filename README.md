# Credit Card Fraud Analysis Dashboard

An interactive Tableau dashboard that explores how fraudulent credit card transactions differ from genuine ones. Built for **PADV Activity 2**.

**Live dashboard:** [View on Tableau Public](https://public.tableau.com/app/profile/rakshitha.v6650/viz/CreditCardFraudDashboard_17932002696680/Dashboard4)
**Dataset:** [Credit Card Fraud Detection on Kaggle](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud)

![Dashboard preview](screenshots/dashboard.png)

---

## Table of contents
1. [Project overview](#project-overview)
2. [Problem statement](#problem-statement)
3. [Dataset description](#dataset-description)
4. [Tools used](#tools-used)
5. [Methodology](#methodology)
6. [Dashboard components](#dashboard-components)
7. [Key insights](#key-insights)
8. [Limitations](#limitations)
9. [Future work](#future-work)
10. [Repository structure](#repository-structure)
11. [References](#references)
12. [Author](#author)

---

## Project overview
Credit card fraud causes financial loss for banks and customers and reduces trust in digital payments. This project turns a large transaction dataset into a one-page dashboard that shows how big the fraud problem is, when it happens, and which transaction features separate fraud from genuine activity.

## Problem statement
Fraud is extremely rare compared with normal spending (about 2 in every 1,000 transactions), so it is hard to notice by eye. The aim of this project is to answer four questions:
1. How big is the fraud problem in terms of count, rate and value?
2. At what times of day is fraud more common?
3. Does the transaction amount affect the chance of fraud?
4. Can the anonymised features V14 and V17 help separate fraud from genuine transactions?

## Dataset description
The dataset is **Credit Card Fraud Detection**, published on Kaggle by the Machine Learning Group of Université Libre de Bruxelles (ULB) and Worldline. It contains transactions made by European cardholders over **two days in September 2013**.

| Item | Value |
|---|---|
| Total transactions | 284,807 |
| Fraud cases | 492 |
| Fraud rate | 0.173% |
| Fraud amount (as shown on the dashboard) | 60,128 |

| Column | Description |
|---|---|
| Time | Seconds elapsed since the first transaction in the dataset |
| Amount | Value of the transaction |
| Class | Label: 0 = genuine, 1 = fraud |
| V1 to V28 | Anonymised features produced by PCA (principal component analysis). Their real meaning is hidden for privacy |

The data is **highly imbalanced**: fraud makes up under 0.2% of all records. The dataset contains no merchant, location or customer identifiers.

> The dataset file (about 150 MB) is not included in this repository because of GitHub's file size limit. Download it from the Kaggle link above.

## Tools used
- **Tableau Public** for data preparation and dashboard design
- **GitHub** for hosting the project files

## Methodology
The CSV file was loaded directly into Tableau and seven calculated fields were created:

| Field | Purpose |
|---|---|
| Class Label | Converts Class (0 or 1) into "Genuine" and "Fraud" |
| Day | Splits the data into Day 1 and Day 2 |
| Hour | Converts elapsed seconds into hour of day (0 to 23) |
| Time Block | Groups hours into six four-hour windows |
| Amount Band | Groups amounts into 0-10, 10-50, 50-200, 200-1000 and 1000+ |
| Fraud Rate | Fraud cases divided by total transactions |
| Fraud Amount | Total value of the fraudulent transactions |

The totals were checked against the published dataset description (284,807 records and 492 fraud cases) before the charts were interpreted.

## Dashboard components
| Component | What it shows |
|---|---|
| KPI cards | Total transactions, fraud cases, fraud rate and fraud amount |
| Fraud vs genuine | Class imbalance between the two groups |
| Transactions per hour, by day | Daily activity pattern for Day 1 and Day 2 |
| V14 vs V17 scatter plot | How fraud separates from genuine transactions on two key features |
| Fraud rate heatmap | Fraud rate for each combination of amount band and time block |
| Amount distribution | How fraud and genuine transactions are spread across amount bands |

## Key insights
1. **Fraud is rare but costly.** Only 0.173% of transactions are fraud, so accuracy alone is a misleading way to judge a detection model.
2. **Fraud rates are higher in the early hours.** The heatmap shows higher rates between hours 0 and 8, when overall activity is lowest. For example, 0.99% for amounts above 1,000 in the first four hours.
3. **Small amounts stand out.** A large share of fraud falls in the 0 to 10 band, consistent with "card testing" behaviour.
4. **Large amounts in quiet hours are riskier.** Transactions above 200 in the early hours show fraud rates several times the overall average.
5. **V14 and V17 help separate fraud.** Fraud points sit away from the dense cluster of genuine transactions, although the groups overlap in the middle.
6. **Some rates are unstable.** High-value bands have few transactions, so one or two fraud cases can change a heatmap cell a lot.

## Limitations
- The data covers only two days from 2013, so it cannot show weekly or seasonal patterns.
- Time is measured from the first transaction, not the real clock time, so hour values are approximate.
- V1 to V28 are anonymised, so the dashboard shows that they separate fraud but cannot explain why.
- There is no merchant, location or customer information.
- The currency of the Amount field is not stated, so no currency symbol is used in the analysis.

## Future work
- Train a classifier (for example logistic regression or random forest) on the data.
- Evaluate it with precision, recall, the precision-recall curve and a confusion matrix.
- Add model panels to the dashboard, such as a threshold control.
- Repeat the analysis on a longer and more recent dataset.

## Repository structure
```
credit-card-fraud-dashboard/
├── screenshots/        Dashboard images
├── Fraud_Transaction_Analysis_Report.docx   Written report
└── README.md           Project description
```

## References
- Machine Learning Group – ULB. (2018). *Credit card fraud detection* [Data set]. Kaggle. https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud
- Dal Pozzolo, A., Caelen, O., Johnson, R. A., & Bontempi, G. (2015). Calibrating probability with undersampling for unbalanced classification. *2015 IEEE Symposium Series on Computational Intelligence*, 159–166.
- Tableau Software. (n.d.). *Tableau Public* [Computer software]. https://public.tableau.com

## Author
**Rakshitha V**


