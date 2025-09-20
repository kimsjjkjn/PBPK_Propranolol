# Results

## Rat IV Model
- in vivo pharmacokinetic data for comparison: doi.org/10.1159/000136352



Figure 1. Rat IV: In Vivo figure from the literature (figure 1 control data was used).


<img width="600" height="800" alt="Screenshot 2025-09-10 at 3 13 19 PM" src="https://github.com/user-attachments/assets/e821a4a7-fc80-422e-940d-2287ed015a3b" />

- Source: doi.org/10.1159/000136352



Figure 2. Rat IV: Predicted vs Digitised In Vivo Propranolol Blood Concentrations.

<img width="468" height="273" alt="image" src="https://github.com/user-attachments/assets/1fd97cfc-5851-4255-b714-438d83ac760e" />

Table 1. Model performance based on concentration–time profile: Average Absolute Fold Error (AAFE) between Predicted and Digitised In Vivo concentrations in the IV rat model
  
| Metric | Value |
| :------ | ----: |
| AAFE | 1.51 |
| Fraction within 2-fold (0.5–2.0) | 0.8 |
| Fraction within 3-fold (0.33–3.0) | 0.8 |

Table 2. Comparison of Predicted Pharmacokinetic Parameters with Literature In Vivo Pharmacokinetic Parameters in IV Rat Model

| Metric             |   Predicted | Literature In Vivo |    Pred/Lit |   FE vs Lit | Within 2x (Lit) | Within 3x (Lit) |
| :----------------- | ----------: | -----------------: | ----------: | ----------: | :-------------: | :-------------: |
| AUC₀–∞ (ng·min/mL) | 30703.66 |             27,122 | 1.13 | 1.13 |       TRUE      |       TRUE      |
| CL (mL/min)        |       81.42 |               92.2 | 0.88 | 1.13 |       TRUE      |       TRUE      |
| Vss (L/kg)         | 5.89 |                5.3 | 1.11 | 1.11 |       TRUE      |       TRUE      |
| t½ (min)           | 46.77 |                 40 | 1.17 | 1.17 |       TRUE      |       TRUE      |

- Abbreviations: AUC, area under the concentration–time curve; CL, clearance; Vss, volume of distribution at steady state; t½, elimination half-life.

Route-level summary (Rat IV)					
- vs Literature: AAFE = 1.14, within 2× = 100%, within 3× = 100%.

Note: 
- Only the parameters reported in the literature were calculated and compared.
- The in vivo time–concentration profile used for Figure 2 and Table 1 was digitised from published figures (as raw Time-Concentration datasets were unavailable). Digitised data are used only for profile-level goodness-of-fit metrics (e.g., AAFE, fold-accuracy). Pharmacokinetic (PK) parameter-level comparisons (Table 2) are made exclusively against literature PK parameter values, because it is more appropriate to benchmark against actual literature data rather than digitised estimates, as digitised values may not fully reflect observed in vivo data (except where digitisation is unavoidable, such as for Time–Concentration profiles).

## Human IV Model
- in vivo pharmacokinetic data for comparison: 10.1371/journal.pone.0097885


Figure 3. Human IV: In Vivo figure from the literature (figure 2A control data was used)
  <img width="711" height="351" alt="Screenshot 2025-09-10 at 2 06 48 PM" src="https://github.com/user-attachments/assets/83b672f8-65d8-4171-b4b3-eead4938a100" />

- Source: 10.1371/journal.pone.0097885

Figure 4. Human IV: Predicted vs Digitised In Vivo Propranolol Plasma Concentrations (in vivo data is in venous plasma concentration, so predicted data was also converted to venous plasma concentration).

<img width="468" height="273" alt="image" src="https://github.com/user-attachments/assets/59f4131f-4722-4d97-82e3-f392feb3212d" />

Table 3. Model performance based on concentration–time profile: Average Absolute Fold Error (AAFE) between Predicted and Digitised In Vivo concentrations in the IV human model

| Metric | Value |
| :------ | ----: |
| AAFE | 1.28 |
| Fraction within 2-fold (0.5–2.0) | 1 |
| Fraction within 3-fold (0.33–3.0) | 1 |

Table 4. Comparison of Predicted Pharmacokinetic Parameters with Literature In Vivo Pharmacokinetic Parameters in IV Human Model

| Metric             |   Predicted | Literature In Vivo |    Pred/Lit |   FE vs Lit | Within 2x (Lit) | Within 3x (Lit) |
| :----------------- | ----------: | -----------------: | ----------: | ----------: | :-------------: | :-------------: |
| AUC₀–∞ (ng·min/mL) | 801.83 |                979 | 0.82 | 1.22 |       TRUE      |       TRUE      |
| CL (mL/min)        | 1247.14 |               1187 | 1.05 | 1.05 |       TRUE      |       TRUE      |
| Vss (L/kg)         | 6.94 |                4.4 |  1.58 |  1.58 |       TRUE      |       TRUE      |
| t½ (min)           |  270.06 |                205 | 1.32 | 1.32 |       TRUE      |       TRUE      |


- Abbreviations: AUC, area under the concentration–time curve; CL, clearance; t½, elimination half-life; Vss, volume of distribution at steady state.

- Note: Human CL reported as total mL/min (70kg standard)

Route-level summary (Human IV)
vs Literature (excluding IV Cmax & Tmax): AAFE = 1.28, within 2× = 100%, within 3× = 100%.


Note: 
- Only the parameters reported in the literature were calculated and compared.
  - In the referenced study, blood sampling was performed only after the infusion ended. This is also evident because the first sampling time point (5 min) shows the maximum observed concentration - if sampling began during the infusion, the end-of-infusion point (10 min) would be expected to capture Cmax. Because the earliest available sample is at 5 min (no sample at t = 0), the literature Tmax defaults to 5 min by design. Direct comparison of Cmax and Tmax with a simulation that reports concentrations from t = 0 would therefore yield misaligned values that are not physiologically informative. Accordingly, Cmax and Tmax were excluded from subsequent parameter analyses and are not reported in this portfolio.
- The in vivo time–concentration profile used for Figure 4 and Table 3 was digitised from published figures (as raw Time-Concentration datasets were unavailable). Digitised data are used only for profile-level goodness-of-fit metrics (e.g., AAFE, fold-accuracy). Pharmacokinetic (PK) parameter-level comparisons (Table 2) are made exclusively against literature PK parameter values, because it is more appropriate to benchmark against actual literature data rather than digitised estimates, as digitised values may not fully reflect observed in vivo data (except where digitisation is unavoidable, such as for Time–Concentration profiles).
  
## Human PO Model
- in vivo pharmacokinetic data for comparison: 10.1371/journal.pone.0097885

Figure 5. Human PO: In Vivo figure from the literature (figure 2B control data was used)
    <img width="711" height="351" alt="Screenshot 2025-09-10 at 2 06 48 PM" src="https://github.com/user-attachments/assets/83b672f8-65d8-4171-b4b3-eead4938a100" />

- Source: 10.1371/journal.pone.0097885

  
Figure 6. Human PO: Predicted vs Digitised In Vivo Propranolol Plasma Concentrations (in vivo data is in venous plasma concentration, so predicted data was also converted to venous plasma concentration).

<img width="480" height="264" alt="image" src="https://github.com/user-attachments/assets/0b8af275-9950-4c06-a528-feb8bc5836c3" />

Table 5. Model performance based on concentration–time profile: Average Absolute Fold Error (AAFE) between Predicted and Digitised In Vivo concentrations in the PO human model

| Metric                            |       Value |
| :-------------------------------- | ----------: |
| AAFE                              | 1.76 |
| Fraction within 2-fold (0.5–2.0)  | 0.58 |
| Fraction within 3-fold (0.33–3.0) | 0.92 |

Table 6. Comparison of Predicted Pharmacokinetic Parameters with Literature In Vivo Pharmacokinetic Parameters in PO Human Model

| Metric             |   Predicted | Literature In Vivo |    Pred/Lit |   FE vs Lit | Within 2x (Lit) | Within 3x (Lit) |
| :----------------- | ----------: | -----------------: | ----------: | ----------: | :-------------: | :-------------: |
| Cmax (ng/mL)       | 17.31 |                 28 | 0.62 | 1.62 |       TRUE      |       TRUE      |
| Tmax (min)         |         100 |                180 | 0.56 |         1.8 |       TRUE      |       TRUE      |
| AUC₀–∞ (ng·min/mL) | 11196.36 |               8930 | 1.25 | 1.25 |       TRUE      |       TRUE      |
| t½ (min)           | 269.99 |                214 | 1.26 | 1.26 |       TRUE      |       TRUE      |
| F (%)              | 34.91 |                 27 | 1.29 | 1.29 |       TRUE      |       TRUE      |

- Abbreviations: AUC, area under the concentration–time curve; Cmax, peak concentration; F, oral bioavailability; t½, elimination half-life; Tmax, time point of Cmax.


Route-level summary (Human PO)
- vs Literature: AAFE = 1.43, within 2× = 100%, within 3× = 100%.



Note: 
- Only the parameters reported in the literature were calculated and compared.
- The in vivo time–concentration profile used for Figure 6 and Table 5 was digitised from published figures (as raw Time-Concentration datasets were unavailable). Digitised data are used only for profile-level goodness-of-fit metrics (e.g., AAFE, fold-accuracy). Pharmacokinetic (PK) parameter-level comparisons (Table 2) are made exclusively against literature PK parameter values, because it is more appropriate to benchmark against actual literature data rather than digitised estimates, as digitised values may not fully reflect observed in vivo data (except where digitisation is unavoidable, such as for Time–Concentration profiles).
