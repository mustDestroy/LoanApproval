# 1. Purpose & Scope
This document records all data cleaning, validation and transformation decisions made during the analysis. The goal is to ensure transparency, reproductability, and defensibility of the modeling process.


# 2. Exploratory Data Analysis
Source: German banking data from 2019 <br>
Domain: Loan approval/Credit risk <br>
Target variable: status <br>


# 3. Data Quality & Data Cleaning decisions
<br>

## 3.1 Numerical features


**Feature:** loan_amount <br>
**Issue Identified:**

**Diagnosis:** <br>

**Decision:**<br>

**Rationale:**
<br><br>

**Feature:** rate_of_interest <br>
**Issue Identified:** <br>
- 35,255 observations with value = -1.0 

**Diagnosis:**
- Sentinel value implying the field not applicable, application rejected before pricing, loan not priced yet (it is a process signal, not a financial one)
- Value magnitude and frequency suggest placeholder indicating missing or non-applicable pricing information, particularly the value itself too frequent and too round compared to real negative rates e.g.  -0.05 or -0.12
- Negative retail interest rates are theoretically plausible in macro finance, but practically implausible for retail loans in this context


**Decision:**
- Reclassify -1.0 as missing (NA)
- Preserve missingness indicator


**Rationale:**
- Prevents leakage
- Aligns with banking workflows
- Improves model validity
<br><br>

**Feature:** interest_rate_spread<br>
**Issue Identified:** <br>

**Diagnosis:** <br>

**Decision:** <br>

**Rationale:** 
<br><br>




**Feature:** term <br>
**Issue Identified:** <br>

**Diagnosis:** <br>

**Decision:** <br>

**Rationale:** 
<br><br>

**Feature:** property_value <br>
**Issue Identified:** <br>

**Diagnosis:** <br>

**Decision:** <br>

**Rationale:** 
<br><br>

**Feature:** income <br>
**Issue Identified:** <br>

**Diagnosis:** <br>

**Decision:** <br>

**Rationale:** 
<br><br>

**Feature:** credit_score <br>
**Issue Identified:** <br>

**Diagnosis:** <br>

**Decision:** <br>

**Rationale:** 
<br><br>

**Feature:** ltv (Loan-To-Value) <br>
**Issue Identified:**


**Diagnosis:** <br>

**Decision:** <br>

**Rationale:** 
<br><br>


**Feature:**  status<br>
**Issue Identified:** <br>

**Diagnosis:** <br>

**Decision:** <br>

**Rationale:** 
<br><br>


**Feature:**  dtir1 <br>
**Issue Identified:** <br>

**Diagnosis:** <br>

**Decision:** <br>

**Rationale:** 
<br><br>


**Feature:** high_interest_rate <br>
**Issue Identified:** <br>

**Diagnosis:** <br>

**Decision:** <br>

**Rationale:** 
<br><br>




**Feature:** senior_age<br>
**Issue Identified:** <br>

**Diagnosis:** <br>

**Decision:** <br>

**Rationale:** <br><br>







# 4. Missingness mechanism assessment (post-cleaning validation)

# 5. Missing value imputation

# 6. Outlier handling rules

# 7. Explicit non-actions
