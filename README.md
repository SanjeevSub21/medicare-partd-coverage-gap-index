# Coverage Gaps and Under-Treatment: Diabetes and Cardiovascular Medication Use in Medicare Part D

A state-level analysis of whether Medicare patients with diabetes and cardiovascular disease receive the medication use we would expect, given how common each disease is in their state.

## Question

When a state has low prescribing, is it because the disease is less common there, or because patients are under-treated? Prescription counts alone cannot separate the two. This project builds a **Coverage Gap Index** that compares actual prescription fills with the fills expected from each state's disease burden.

## Data (all public, from CMS)

| Ingredient | Source | Year |
|---|---|---|
| Medication use | Medicare Part D Prescribers by Geography and Drug | 2024 |
| Population | Medicare Monthly Enrollment | 2024 |
| Disease burden | Mapping Medicare Disparities tool | 2023 |

Coverage: 50 states and the District of Columbia.

Drug groups analysed:
- **Diabetes:** metformin, insulin, SGLT-2 inhibitors, GLP-1 agonists, DPP-4 inhibitors (195.6M fills)
- **Cardiovascular:** statins, ARBs, ACE inhibitors (601.1M fills)

## Method

1. **Patients** = disease prevalence × Part D beneficiaries
2. **Expected fills** = patients × national fills per patient
3. **Coverage Gap Index (ratio method)** = actual fills ÷ expected fills
4. **Regression method:** fit fills per patient = β₀ + β₁ × prevalence + ε, then index = actual ÷ predicted fills per patient
5. **Shortfall** = expected fills − actual fills
6. States with an index below **0.80** are flagged as a possible coverage gap

The two methods are compared using Spearman rank correlation and the overlap of their ten lowest states.

## Key results

| | Diabetes | Cardiovascular |
|---|---|---|
| Index range (ratio method) | 0.83 to 1.22 | 0.80 to 1.57 |
| States below 1.00 | 27 | 18 |
| States flagged below 0.80 | 0 | 1 (Oklahoma) |
| Slope of fills per patient on prevalence | −0.07 (p = 0.14, R² = 0.04) | −1.97 (p < 0.001, R² = 0.72) |
| Spearman correlation between methods | 0.97 | 0.39 |
| Overlap of ten lowest states | 9 of 10 | 4 of 10 |
| Estimated missing fills | 4.42M | 28.93M |

- Diabetes shows a mild, widespread gap; the two methods agree.
- Cardiovascular shows a stronger gap in high-burden states, and the two methods disagree, so results should be read with both.
- Five states appear among the lowest in both conditions: **Delaware, Oklahoma, New Jersey, Florida and Arkansas**.

<img width="1800" height="1140" alt="us_map_gap_states" src="https://github.com/user-attachments/assets/8882cae2-60d4-49d1-96ab-39d3ea27a678" />


## Limitations

- Disease burden is from 2023 and prescription use is from 2024, the latest years available for each source.
- The data are state-level, so results describe states, not individual patients.
- Part D fills do not capture medicines paid outside Part D.
- The analysis measures gaps in use relative to expected use; it does not establish causes.

## Tools

Python (pandas, NumPy, SciPy, Matplotlib)

## Author

Sanjeev Subramaniam, MSc Business Analytics, Manipal School of Commerce and Economics, MAHE
