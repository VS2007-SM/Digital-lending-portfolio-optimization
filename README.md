# 📊 Digital Lending: Portfolio Optimization

> **Reduced portfolio default rate from 42.5% → ~27% while retaining 75–80% of loan volume.**  
> An end-to-end Data Science consulting project — from synthetic dataset generation to a full credit policy framework.

---

## 🏆 Key Results at a Glance

| Metric | Before Policy | After Policy |
|--------|--------------|--------------|
| Portfolio Default Rate | 42.5% | ~27% |
| Grade F/G Loan Volume | 865 loans | ~100 loans |
| Agent Channel Default Rate | 47.7% | ~40% (est.) |
| Grade A–C Approval Share | ~25% | >40% |
| Best Model AUC | — | 0.6985 (Logistic Regression) |

---

## 📌 Project Overview

This project was developed under the **Consulting & Analytics Club, IIT Guwahati** as a consulting-style engagement. The challenge: design a **data-driven credit policy framework** for a digital lending institution — from scratch.

**Problem Statement:**
> How can a digital lending institution leverage end-to-end customer and transaction data to strengthen credit risk assessment, enable early detection of delinquencies, optimise pricing and product strategies, and drive sustainable, risk-adjusted portfolio growth?

**Team:** Vivek Shende· Ishank Sachan · Rahul Ahirwar  
**Organisation:** Consulting & Analytics Club, IIT Guwahati  
**Date:** June 2026

---

## 🔑 Most Counterintuitive Finding

| Grade | Expected Revenue/Loan | Default Rate |
|-------|----------------------|--------------|
| Grade C | ₹14,154 | 26.8% ✅ |
| Grade F | ₹14,233 | 60.4% ❌ |
| Grade G | ₹14,867 | 62.1% ❌ |

**Grade F & G offer only marginal extra revenue over Grade C — at more than twice the default risk.**  
Chasing riskier borrowers doesn't grow a portfolio. It quietly destroys it.

---

## 🗂️ Repository Structure

```
digital-lending-portfolio/
│
├── README.md                          ← You are here
│
├── notebook/
│   └── Digital_Lending_Notebook.ipynb ← Full ML pipeline (Google Colab)
│
├── data/
│   └── digital_lending_synthetic.csv  ← 10,000-row synthetic dataset (21 features)
│
├── dashboard/
│   └── Dashboard.html                 ← Interactive HTML dashboard (open in browser)
│
├── reports/
│   ├── Credit_Policy_Report_Final.pdf ← Main deliverable (addressed to CRO)
│   └── README_Documentation.pdf       ← Full technical documentation
│
└── presentation/
    └── Digital_Lending_Presentation.pdf ← 10-slide stakeholder deck
```

---

## ⚙️ How to Run the Notebook

**Recommended: Google Colab (free, no setup)**

1. Go to [colab.research.google.com](https://colab.research.google.com)
2. Click **Upload** → Select `Digital_Lending_Notebook.ipynb`
3. Click **Runtime → Run All**
4. The synthetic dataset is auto-generated in Cell 1 — no external download needed
5. All charts render inline; download outputs via the final cell

**Required Libraries** (pre-installed on Colab):
```
pandas · numpy · matplotlib · seaborn · scikit-learn · xgboost · shap
```

**For local setup:**
```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost shap
```

> ✅ **Fully reproducible:** All random seeds set to `42`. Running the notebook top-to-bottom always produces identical results.

---

## 📊 Dashboard

Open `dashboard/Dashboard.html` in any browser — **no internet required, no installation.**

**Dashboard contains:**
- Default Rate by Grade (bar chart)
- Default Rate by Channel (bar chart)
- CLV vs Risk Scatter by Employment Type
- Expected Revenue by Grade
- Early Warning KPI Table
- Portfolio Summary Statistics

Tested on Chrome, Firefox, and Edge.

---

## 🔬 Analytical Pipeline

```
Synthetic Data Generation
        ↓
Exploratory Data Analysis (6 analytical charts)
        ↓
Gap Analysis (defaulters vs fully paid — 6 key metrics)
        ↓
Feature Engineering (installment_to_income, grade_num, encodings)
        ↓
Predictive Modelling
  ├── Logistic Regression  → AUC: 0.6985
  └── XGBoost              → AUC: 0.6933
        ↓
SHAP Feature Attribution (top default predictors)
        ↓
CLV & Revenue Analysis (expected revenue per grade)
        ↓
Credit Policy Framework Design
        ↓
Impact Quantification
```

---

## 🧮 Dataset Description

| Specification | Value |
|---------------|-------|
| Total Rows | 10,000 loan records |
| Total Features | 21 columns |
| Target Variable | `default` (1 = defaulted, 0 = fully repaid) |
| Overall Default Rate | 42.5% (stress-test design) |
| NTC Customers | 3,488 (34.88%) |
| Random Seed | 42 (fully reproducible) |

**7 Data Areas:** Customer Profile · Loan & Product · Repayment Behaviour · Behavioural Signals · Acquisition Channel · Time Dimension · Outcomes

> **Note on default rate:** The 42.5% rate is intentional — a stress-test design to enable policy framework development across all risk segments including Grade E–G. In live production portfolios, default rates typically range 2–8%. Risk differentials and policy recommendations remain directionally valid.

---

## 🛡️ Credit Policy Framework (Summary)

| Grade | Decision | Max Loan | Max Tenure | Key Condition |
|-------|----------|----------|------------|---------------|
| A | ✅ Approve | No cap | 36 months | Loyalty pricing eligible |
| B | ✅ Approve | ₹3,00,000 | 36 months | Standard terms |
| C | ✅ Approve | ₹75,000 | 24 months | Rate ceiling 20% |
| D | ⚠️ Conditional | ₹50,000 | 18 months | DTI < 0.45 + income proof |
| E | 🔴 Restricted | ₹25,000 | 12 months | Salaried only |
| F | ❌ Decline | — | — | Salaried + FICO > 640 only |
| G | ❌ Decline | — | — | Decline all |

**Key Guardrails:** DTI hard cap 0.65 · Installment/Income ≤ 40% · Spending shock → manual review

---

## 🚨 Early Warning System

| Tier | Trigger | Action | Review Cycle |
|------|---------|--------|--------------|
| 🟡 WATCH | DTI > 0.50 OR spending_shock = 1 | Flag + repayment reminder | Monthly |
| 🟠 ALERT | DTI > 0.55 AND (ITI > 0.35 OR volatility > 0.75) | Outreach + restructuring offer | Bi-weekly |
| 🔴 CRITICAL | Grade ≥ E AND DTI > 0.55 AND spending_shock = 1 | Immediate escalation to collections | Weekly |

---

## 👥 New-to-Credit (NTC) Framework

**3,488 customers (34.88%) have no formal bureau history** — affecting a customer base representative of 190 million Indians underserved by traditional credit scoring.

**NTC Qualifying Criteria (all 3 must pass):**
1. Installment-to-Income Ratio < 0.35
2. DTI < 0.50
3. Employment: Salaried or Self-Employed only

**Pathway:** ₹30,000 starter loan (12-month tenure) → 2 successful repayments → Graduate to standard grade framework

---

## 🏅 SHAP — Top Default Predictors

| Rank | Feature | Business Interpretation |
|------|---------|------------------------|
| #1 | Interest Rate | High rate increases repayment burden — feeds the default cycle |
| #2 | DTI | Debt burden vs income — key liquidity stress indicator |
| #3 | Employment Type | Informal/Student segments have unstable income streams |
| #4 | Cash Flow Volatility | Irregular income directly raises repayment risk |
| #5 | Acquisition Channel | Agent channel carries adverse selection risk |

**The Rate-Trap:** Interest rate → higher DTI → higher default → even higher rate assigned. Breaking this cycle with tiered rate caps for Grade D borderline borrowers is the single highest-impact policy lever.

---

## 📦 Deliverables

| File | Description |
|------|-------------|
| `Credit_Policy_Report_Final.pdf` | 9-section report addressed to the Chief Risk Officer |
| `Digital_Lending_Presentation.pdf` | 10-slide stakeholder presentation deck |
| `Digital_Lending_Notebook.ipynb` | Full Python ML pipeline on Google Colab |
| `digital_lending_synthetic.csv` | 10,000-row synthetic dataset (21 features) |
| `Dashboard.html` | Self-contained interactive HTML dashboard |
| `README_Documentation.pdf` | Full technical documentation |

---

## 🎓 Acknowledgement

Developed under the **Consulting & Analytics Club, IIT Guwahati** project programme.  
Certificate of Participation awarded to the project team.

---

## 🤝 Connect

**Vivek** · [LinkedIn](https://www.linkedin.com/in/vivek-shende-259b96380) · [GitHub](https://github.com/VS2007-SM) · [Repo](https://github.com/VS2007-SM/Digital-lending-portfolio-optimization)   
**Ishank Sachan** · [LinkedIn](https://www.linkedin.com/in/ishank-sachan-a50119379)  
**Rahul Ahirwar** · [LinkedIn](#)

---

*Built with Python · XGBoost · SHAP · Logistic Regression · Plotly · Google Colab*
