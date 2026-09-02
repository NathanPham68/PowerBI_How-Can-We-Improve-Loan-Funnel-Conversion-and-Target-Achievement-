# [POWER BI] How Can We Improve Loan Funnel Conversion and Target Achievement? - Consumer Lending

<img width="1200" height="900" alt="image" src="https://github.com/user-attachments/assets/6cecb8cc-46f1-4fea-96a3-4532783d48de" />

> **End-to-end BI project for analyzing the digital consumer-loan funnel, marketing conversion, branch/product performance, target achievement, and portfolio repayment indicators.**

---

## 📌 Project Overview

Bank **X** is developing an online consumer-lending channel and collects customer data across multiple stages of the lending journey.

This project builds a **multi-view Loan Funnel Dashboard** that combines:

- 📣 Marketing lead acquisition
- 🧾 Loan applications
- ✅ Credit approvals
- 💸 Loan disbursements
- 🎯 Target vs. actual performance
- 💳 Portfolio repayment and outstanding-balance monitoring

**Loan Funnel Dashboard** is a business intelligence case study demonstrating how multiple lending and marketing data sources can be integrated into a single analytical framework.

The project focuses on turning raw funnel data into actionable management views across **acquisition, conversion, credit processing, disbursement, target achievement, and portfolio monitoring**.

> ⚠️ **Data disclaimer:** All data used in this project are **synthetic / assumed data created for analytical practice**. The findings below describe the supplied dataset only and should not be interpreted as the actual performance of a real bank, branch, product, or marketing channel.

---

## 🎯 Business Objectives

The dashboard is designed to answer five key questions:

1. **How effectively are marketing leads converted into loan leads?**
2. **Where does the loan funnel experience the largest drop-off?**
3. **Which branches, products, channels, and campaigns perform better?**
4. **How does actual disbursement compare with the assigned target?**
5. **What additional portfolio indicators can be monitored after disbursement?**

---

## 🗂️ Data Model

### Fact Tables

| Table | Business Meaning | Key Role |
|---|---|---|
| `FACT_LEAD_SIGNUP_RAW` | Raw marketing / digital leads | Marketing acquisition |
| `FACT_LOAN_LEAD` | Loan leads | Funnel entry |
| `FACT_LOAN_APPLICATION` | Loan applications | Application stage |
| `FACT_LOAN_APPROVAL` | Credit decisions | Approval stage |
| `FACT_LOAN_DISBURSEMENT` | Actual disbursements | Final funnel stage |
| `FACT_LOAN_TARGET` | Monthly disbursement targets | Target comparison |

### Dimension Tables

| Table | Business Meaning |
|---|---|
| `DIM_LOAN_PRODUCT` | Loan product, category, and customer segment |
| `DIM_BRANCH` | Branch, region, and area hierarchy |
| `DIM_DATE` | Common calendar dimension for all relevant dates |

### 🔗 Funnel Flow

```text
Marketing Lead
     │
     ▼
Loan Lead
     │
     ▼
Application
     │
     ▼
Approval
     │
     ▼
Disbursement
```

---

## 🔄 Data Mapping & Matching Logic

### Marketing → Loan Lead

The project uses the proposed business rule:

> A marketing lead is considered matched to a loan lead when the records align on **ProductID** and the **Loan Lead date is greater than or equal to the Marketing Signup Date**.

This rule is intentionally documented because the raw marketing dataset does not provide a direct `LoanLeadID` relationship.

```text
FACT_LEAD_SIGNUP_RAW
(CustomerID, ProductID, Branch, SignupDate)
              │
              │ ProductID + date condition
              ▼
FACT_LOAN_LEAD
(LeadID, CustomerID, ProductID, Branch, SignupDate)
```

### Loan Funnel Relationships

```text
FACT_LOAN_LEAD
      │ LeadID
      ▼
FACT_LOAN_APPLICATION
      │ ApplicationID
      ▼
FACT_LOAN_APPROVAL
      │ LeadID / LoanID
      ▼
FACT_LOAN_DISBURSEMENT
```

### Common Dimensions

```text
DIM_LOAN_PRODUCT ─────► ProductID
DIM_BRANCH ───────────► Branch
DIM_DATE ─────────────► Signup / Application / Approval / Disbursement Date
```

---

## 🧠 Analytical Approach

The dashboard follows a funnel-oriented analytical framework:

```text
Acquisition
    ↓
Marketing Lead
    ↓
Loan Lead
    ↓
Application
    ↓
Approval
    ↓
Disbursement
    ↓
Target Achievement
    ↓
Repayment / Portfolio Monitoring
```

This allows management to move from a high-level performance view to the specific stage where volume or value is lost.

---

## 🛠️ Tools & Skills Demonstrated

- 📊 Business Intelligence & Dashboard Design
- 🧮 KPI & Measure Definition
- 🔗 Data Modeling
- 🧹 Data Integration & Transformation
- 🏦 Loan Funnel Analytics
- 📣 Marketing Funnel Analytics
- 🎯 Target vs Actual Analysis
- ⏱️ Process / Time-to-Disbursement Analysis
- 💳 Portfolio & Repayment Analytics
- 🔍 Root-cause-oriented Business Analysis
- 📈 Interactive Reporting

---

## 📊 Dashboard Views

### 1️⃣ View 1 — Marketing Lead & Conversion

#### Purpose

Analyze marketing lead acquisition and the conversion from **Marketing Lead → Loan Lead**.

#### Main KPIs

- 📣 Total Marketing Leads
- 🏦 Total Loan Leads
- 🔄 Marketing → Loan Lead Conversion Rate
- ⏱️ Average Lead-to-Application Days
- 📈 Average Leads per Campaign

#### Main Visuals

- Marketing leads and conversion trend over time
- Marketing leads by day of week
- Marketing lead heatmap by month and campaign
- Marketing leads by channel
- Marketing leads by campaign
- Marketing leads by branch
- Loan leads by branch
- Marketing → Loan Lead funnel
- Conversion heatmap by channel and branch

<img width="1200" height="755" alt="image" src="https://github.com/user-attachments/assets/4b3c5c20-8de0-4ac9-903b-ed2c8f938498" />

#### Observed Result from the Supplied Synthetic Dataset

The dashboard shows approximately **4,000 marketing leads** and **3,000 loan leads**, with a marketing-to-loan-lead conversion rate of approximately **23.9%** in the dashboard.

This indicates a substantial gap between the overall marketing lead pool and the leads that enter the loan funnel. Based on the supplied synthetic data, this is an area worth investigating by channel, campaign, branch, and product.

> **Important:** A low conversion rate does not by itself prove poor marketing performance. Lead quality, eligibility criteria, duplicate handling, matching logic, and credit-policy effects should also be investigated before drawing a business conclusion.

---

### 2️⃣ View 2 — Loan Funnel Performance

#### Purpose

Track the complete lending journey:

**Lead → Application → Approval → Disbursement**

#### Main KPIs

- 👥 Total Leads
- 📝 Total Applications
- ✅ Total Approvals
- 💸 Total Disbursements
- 💰 Total Disbursed Amount

#### Main Visuals

- Funnel conversion: Lead → Application → Approval → Disbursement
- Average days from Signup → Disbursement by branch
- Average processing time by loan category
- Loan funnel trend over time
- Category efficiency scatter plot
- Time-to-disbursement distribution
- Revenue / amount leakage analysis
- Branch performance matrix

<img width="1200" height="757" alt="image" src="https://github.com/user-attachments/assets/a079c6dc-cf4b-4301-9c63-81cacde5eb31" />

#### Observed Result from the Supplied Synthetic Dataset

The dashboard shows:

| Funnel Stage | Volume |
|---|---:|
| Lead | 3,000 |
| Application | 2,247 |
| Approval | 1,189 |
| Disbursement | 577 |

The largest volume reduction occurs around the **Application → Approval** stage, followed by the **Approval → Disbursement** stage.

For the synthetic dataset, this suggests that credit approval and post-approval conversion deserve priority investigation.

Possible analytical hypotheses include:

- incomplete or unsuitable application information;
- customer eligibility issues;
- credit-policy rules;
- approved customers not completing the disbursement process;
- operational or process delays.

These are **hypotheses for further investigation**, not conclusions proven by the supplied data.

#### ⏱️ Time-to-Disbursement

The dashboard indicates that a large share of disbursements falls within the **0–14 day** range from signup to disbursement.

This suggests that most observed cases move through the funnel within a relatively short period, although the exact operational SLA should be compared with the bank's actual policy if this were production data.

---

### 3️⃣ View 3 — Target vs. Actual

#### Purpose

Compare actual loan disbursement performance with the assigned monthly target.

#### Core Metrics

**Actual Disbursement Amount**

```text
SUM(FACT_LOAN_DISBURSEMENT[DisbursementAmount])
```

**Target Amount**

```text
SUM(FACT_LOAN_TARGET[TargetDisbursement])
```

**Achievement Rate**

```text
Actual Disbursement Amount / Target Amount
```

**Target Gap**

```text
Target Amount - Actual Disbursement Amount
```

#### Main Visuals

- Monthly Target vs Actual
- Achievement % by branch
- Target vs Actual by branch
- Target gap breakdown
- Target vs Actual matrix
- Monthly branch-level breakdown

<img width="1200" height="757" alt="image" src="https://github.com/user-attachments/assets/98651f17-7f32-4f10-b7bb-0c214adb69ad" />

#### Observed Result from the Supplied Synthetic Dataset

The dashboard reports approximately:

- 💸 **Actual Disbursement:** 87B
- 🎯 **Target:** 4.05T
- 📊 **Achievement:** approximately **2.16%**

The supplied data therefore show a **very large gap between actual disbursement and target**.

This should be treated as a descriptive finding about the synthetic dataset. Before interpreting it as a business problem, the target scope, target grain, date coverage, product coverage, and aggregation logic should be validated.

---

### 4️⃣ View 4 — Repayment & Outstanding Balance

> **Optional extension requested in the project brief**

The project extends the original funnel dashboard with repayment-related information from an additional:

`FACT_LOAN_REPAYMENT`

#### Purpose

Monitor the portfolio after disbursement and provide a starting point for credit-risk and portfolio-management analysis.

#### Main KPIs

- 💳 Current Outstanding Balance
- 💰 Total Principal Repaid
- 📈 Collection Efficiency
- ⚠️ NPL Ratio
- 💵 Interest Income

<img width="1200" height="702" alt="image" src="https://github.com/user-attachments/assets/5eb65501-aa67-45b1-a19e-fbb8026f187a" />

#### Main Visuals

- Outstanding balance by debt group
- Outstanding balance by month
- Scheduled vs actual repayment trend
- Outstanding balance by loan product
- Customer segment risk
- Risk matrix by month and branch

#### Example Portfolio Indicators

**Outstanding Balance**

```text
Current Outstanding Balance
= Principal Outstanding at the selected reporting date
```

**Principal Repaid**

```text
Total Principal Repaid
= Cumulative Principal Repaid
```

**Collection Efficiency**

```text
Collection Efficiency
= Actual Repayment / Scheduled Repayment
```

**NPL Ratio**

```text
NPL Ratio
= Non-performing Outstanding Balance / Total Outstanding Balance
```

The repayment view is an extension of the original funnel analysis and would require the additional repayment fact table and clearly defined business rules before being used for production reporting.

---

## 🔍 Key Insights

Based strictly on the **synthetic data and dashboard outputs supplied for this project**:

1. 📣 **Marketing → Loan Lead:** Around **4,000 marketing leads** are shown against approximately **3,000 loan leads**, with a reported conversion rate of about **23.9%**. The difference suggests an opportunity to examine lead quality and channel/campaign effectiveness.

2. 🔎 **Channel & Campaign Optimization:** Channels with relatively high lead volumes should not automatically be considered successful. Conversion performance should be evaluated together with lead volume, branch, campaign, product, and downstream disbursement.

3. 🧾 **Funnel Leakage:** The largest observed drop-off is between **Application and Approval**, followed by **Approval and Disbursement**. These stages are therefore the most important areas for further diagnostic analysis.

4. 🏢 **Branch Performance:** The supplied dashboard shows **Ho Chi Minh City and Hanoi branches** among the stronger branches in terms of loan-lead/application/disbursement volume. This reflects volume performance in the synthetic dataset, not necessarily branch productivity or profitability.

5. ⏱️ **Time-to-Disbursement:** Most observed disbursements fall within the **0–14 day** ranges, suggesting relatively short observed processing times for a large share of cases.

6. 🎯 **Target Achievement:** Actual disbursement is approximately **87B versus a 4.05T target**, producing an achievement rate of roughly **2.16%**. The gap is substantial and should trigger validation of target definitions, data coverage, and performance drivers.

7. 📊 **Overall Recommendation:** The most useful next analytical step would be to connect **marketing quality → application quality → credit decision → disbursement**, rather than evaluating each stage independently.


> **All conclusions are based on the synthetic dataset supplied with this project.**
