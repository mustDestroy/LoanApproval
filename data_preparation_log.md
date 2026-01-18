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
- No data quality issues identified

**Diagnosis:** <br>
- The 'loan_amount' expresses the principal exposure of the bank to the borrower
- The oberved values fall in a range [16500; 3576500]
- This range is consistent with realistic lending scenarios as retail mortgages and high-value loan products
- No observation represent zeros, negatives or implausible values

**Decision:**<br>
- No data cleaning action required
- Values are kept without transformation

**Rationale:**
- Observed values align with standard banking practices and credit exposure definitions
- Preserving the original values maintains the economic interpretability and predictive information for downstream credit risk modeling


<br><br>

**Feature:** rate_of_interest <br>
**Issue Identified:** <br>
- 35,255 observations with value = -1.0 

**Diagnosis:**
- The 'rate_of_interest' is the amount charged for borrowing money from the bank expressed in percentages
- In banking, LTV above 100% are very unusual,  LTV above 200% are economically implausible
- The observed values fall within range [-1.0; 8.0]
- The 35,255 observations with -1.0 are sentinel values imply the field is not applicable, application rejected before pricing or loan not priced yet (it is a process signal, not a financial one)
- Value magnitude and frequency of the sentinel values suggest placeholder indicating missing or non-applicable pricing information, particularly the value itself too frequent and too round compared to real negative rates e.g.  -0.05 or -0.12
- Negative retail interest rates are theoretically plausible in macro finance, but practically implausible for residental loans in this context


**Decision:**
- Reclassify -1.0 as missing (NA)
- Preserve missingness indicator to keep process signals


**Rationale:**
- Prevents leakage
- Aligns with banking workflows
- Excluding economically implausible values prevents model distortion

<br><br>

**Feature:** interest_rate_spread<br>
**Issue Identified:** <br>
- No data quality issues identified

**Diagnosis:** <br>
- The 'interest_rate_spread' represents the difference between the applied loan interest rate and benchmark rate. Expressed as percentages.
- The observed values fall within range [-3.638; 3.357]
- Negative spreads are economically plausible and indicate that the loan is priced below the benchmark. It can happen due to promotional pricing, borrower's creditworthiness
- Values are consistent with realistic retail banking scenarios
- No implausible extremes were observed.

**Decision:** <br>
- No data cleaning action required

**Rationale:** 
- The variable aligns with standard banking definitions and practices
- Preserving the original values maintains the economic interpretability and predictive information of the feature

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
- 1233 observations with value = 0.0

**Diagnosis:** <br>
- The 'income' represents net monthly income since DTIR calculation requires monthly income as a standard (unit ambiguity is also resolved empirically in income_frequency.txt)
- The income values are discretized in steps of 60 (bucketed values e.g. 60, 120, 180)
- The 1233 zero-income observations are sentinel values rather than true zero income. These likely to represent that the client did not declare his income or income verification is pending or system default.
- The observed non-zero values fall in range [60.0; 578580] forming an extensive and econimically plausible distribution
- While very low income values occur in the dataset and might appear economically weak, they remain plausible in case of joint applications, subsidized loans, incomplete income reporting
- The magnitude and frequency of income values upper the sanity bound represent economically plausible incomes
- Extremely high values are rare, but economically plausible which is not a data quality issue (e.g. business owners, high-net-worth individuals)


**Decision:** <br>
- Reclassify 0.0 as missing (NA)
- Retain all positive income values without executing a hard lower cutoff
- Do not cap high income values 
- Preserve missingness indicator to retain process signals

**Rationale:** 
- Zero-income values distort DTIR calculations and do not illustrate economic reality
- Preserving the whole non-zero income range maintains economic interpretability and allows model to learn risk relationships organically
- Avoiding an aggressive lower sanity bound prevents incorrect exclusion of valid but incomplete or joint-application cases.


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
- The observed values fall within range [ 0.967478198; 7831.25]
- The observation with LTV ~0.97 is consistent with unit inconsistency (ratio stored instead of percentage)
- The 6 observations represent absurd percentages (>300%) => these are data errors
- Such small number of observations suggest the issue is not systematic
- Extreme values are likely to be caused by sentinel / fallback calculations in the bank's workflow
- 'ltv' and 'property_value' have a strong relationship

**Decision:** <br>
- Values that are element of interval [0,1) multiplied by 100 to comply with unit consistency
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
