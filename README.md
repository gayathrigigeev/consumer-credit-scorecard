# Consumer Credit Scorecard Model

Identifying key drivers of loan default using logistic regression on the Lending Club consumer loans dataset.

---

## Background

Understanding what drives loan default is fundamental to responsible lending. This project builds a probability-of-default (PD) scorecard that predicts whether a borrower is likely to default based on information available at the time of application - mirroring the credit assessment process used by consumer lenders.

---

## Dataset

- **Source:** Lending Club loan dataset (publicly available on Kaggle)
- **Full dataset:** 2.26 million loans
- **Sample used:** 1 million loans (sampled for computational efficiency)
- **Default rate:** ~25.2%
- **Target variable:** Binary — 1 = defaulted, 0 = fully repaid

Loans with ambiguous outcomes (currently active or in grace period) were excluded to ensure integrity of the target variable.

---

## Methodology

- **Model:** Logistic regression (baseline industry-standard technique for credit scorecard development)
- **Features:** 19 application-time variables including loan grade, debt-to-income ratio, employment length, delinquency history, revolving credit utilisation, and loan purpose
- **Data leakage prevention:** Only features observable at application time were included — no post-origination data used
- **Encoding:** One-hot encoding applied to categorical variables
- **Validation:** 80/20 train-test split with fixed random state

---

## Key Findings

**Default rate by loan grade**
Default rates rose consistently from 8.2% at grade A to 58.9% at grade G - confirming the grading system has strong discriminatory power.

**Default rate by DTI band**
Borrowers with DTI above 40 defaulted at 37% - more than double the rate of borrowers with DTI below 10 at 19%. DTI is confirmed as a meaningful risk indicator.

**Default rate by loan purpose**
Small business loans showed the highest default rate at 37.1%, likely reflecting cash flow volatility. Credit card and car loans showed the lowest rates.

---

## Results

| Metric | Score | Benchmark |
|--------|-------|-----------|
| Gini   | 0.316 | Acceptable (>0.25) |
| KS     | 0.237 | Acceptable (>0.20) |

**Key risk drivers identified (by coefficient strength):**
- Credit enquiries in last 6 months (inq_last_6mths) — strongest positive predictor
- Loan term — 60 month loans carry significantly higher default risk
- Recent delinquency history — past behaviour predicts future behaviour
- Loan grade — grades D and above show increasing default probability

**Note on sample size:** Gini ranged between 0.316–0.385 across different sample sizes tested (100k–1M rows). Variance is expected behaviour for a baseline logistic regression model. The 1 million row sample was selected as the most representative within available computational constraints.

---

## How to Run

1. Download the Lending Club dataset from Kaggle
2. Place `loan.csv` in the same folder as the notebook
3. Open `sme_credit_scorecard.ipynb` in Jupyter Notebook
4. Run all cells from top to bottom

**Requirements:**
---

pandas
numpy
matplotlib
scikit-learn
scipy

---

Install with:
---

pip install pandas numpy matplotlib scikit-learn scipy

---

---

## Next Steps

- Implement random forest model to target Gini above 0.40
- Feature engineering — interaction terms between grade and DTI
- Build an interactive credit policy tool — set a threshold and see approve/decline rates in real time

---

## Author

**Gayathri Gigeev**
MSc Finance and Financial Technology — Henley Business School (Distinction)
Credit Analyst 
[LinkedIn](https://www.linkedin.com/in/gayathri-gigeev/)
