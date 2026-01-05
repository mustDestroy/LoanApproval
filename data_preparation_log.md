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
- Negative retail interest rates are theoretically plausible in macro finance, but practically implausible for residental loans in this context


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
- No data quality issues identified

**Diagnosis:** <br>
- The 'interest_rate_spread' represents the difference between the applied loan interest rate and benchmark rate
- The observed values fall within range [-3.638, 3.357]
- Negative spreads are economically plausible and indicate that the loan is priced below the benchmark. It can happen due to promotional pricing, borrower's creditworthiness
- Values are consistent with realistic retail banking scenarios
- No implausible extremes were observed.

**Decision:** <br>
- No data cleaning action required

**Rationale:** 
- The variable aligns with standard banking definitions and practices
- Preserving the original values maintains the economic interpretability and predictive information of the feature.

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
- 1 observation where value < 1% (value = 0.967478198) 
- 6 observations where value > 300% 

**Diagnosis:** <br>
- LTV is defined as the ratio of loan amount to property value, typically expressed as a percentage. 
- In retail, LTV above 100% are very unusual,  LTV above 200-300% are economically implausible
- The observation with LTV ~0.97 is consistent with unit inconsistency (ratio stored instead of percentage)
- The 6 observations represent absurd percentages (>300%) => these are data errors
- Such small number of observations suggest the issue is not systematic
- Extreme values are likely to be caused by sentinel / fallback calculations in the bank's workflow
- 'ltv' and 'property_value' have a strong relationship

**Decision:** <br>
- Values that are element of interval (0,1) multiplied by 100 to comply with unit consistency
- Values exceeding 300% are reclassified as missing (NA)
- Preserve missingness indicators to keep invaluable process signals

**Rationale:** 
- The variable aligns with standard banking definitions and practices
- Excluding economically implausible values prevents model distortion 


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
