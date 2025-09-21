# Results

## Rat IV (Intravenous Administration) Model
- In vivo pharmacokinetic data for comparison: doi.org/10.1159/000136352



Figure 1. In vivo propranolol blood concentration versus time profiles after intravenous application in healthy rat from the literature (figure 1 control data was used).

<img width="600" height="800" alt="Screenshot 2025-09-22 at 1 38 47 AM" src="https://github.com/user-attachments/assets/4a19c3ab-637c-4650-98b0-cc14193bb2de" />

- Source: doi.org/10.1159/000136352



Figure 2. In vivo vs predicted time-concentration graph of intravenously administered propranolol to healthy rat.


<img width="468" height="273" alt="image" src="https://github.com/user-attachments/assets/1fd97cfc-5851-4255-b714-438d83ac760e" />

Table 1. Model performance based on time-concentration profile: Average Absolute Fold Error (AAFE) between predicted and digitised in vivo concentrations in rat IV model.
  
| Metric | Value |
| :------ | ----: |
| AAFE | 1.51 |
| Fraction within 2-fold (0.5–2.0) | 0.8 |
| Fraction within 3-fold (0.33–3.0) | 0.8 |

Table 2. Comparison of predicted pharmacokinetic parameters with literature in vivo pharmacokinetic parameters in rat IV model.

| Metric             |   Predicted | Literature In Vivo |    Pred/Lit |   FE vs Lit | Within 2x (Lit) | Within 3x (Lit) |
| :----------------- | ----------: | -----------------: | ----------: | ----------: | :-------------: | :-------------: |
| AUC₀–∞ (ng·min/mL) | 30703.66 |             27122 | 1.13 | 1.13 |       TRUE      |       TRUE      |
| CL (mL/min)        |       81.42 |               92.2 | 0.88 | 1.13 |       TRUE      |       TRUE      |
| Vss (L/kg)         | 5.89 |                5.3 | 1.11 | 1.11 |       TRUE      |       TRUE      |
| t½ (min)           | 50.17 |                 40 | 1.25 | 1.25 |       TRUE      |       TRUE      |

- Abbreviations: AUC, area under the concentration–time curve; CL, clearance; Vss, volume of distribution at steady state; t½, elimination half-life.

Table 3. Model performance based on PK parameters: Average Absolute Fold Error (AAFE) between predicted and literature in vivo PK parameters in rat IV model.

| Metric | Value |
| :------ | ----: |
| AAFE | 1.16 |
| Fraction within 2-fold (0.5–2.0) | 1.0 |
| Fraction within 3-fold (0.33–3.0)| 1.0 |

Note: 
- Only the parameters reported in the literature were calculated and compared.
- The in vivo time–concentration datasets used for Figure 2 and Table 1 were digitised from published figures (as raw time-concentration datasets were unavailable). Digitised data are used only for plotting time-concentration profile and profile-level goodness-of-fit metrics (e.g., AAFE, fold-accuracy). Pharmacokinetic (PK) parameter-level comparisons (Table 2 and 3) are made exclusively against literature PK parameter values, because it is more appropriate to benchmark against actual literature data rather than digitised estimates, as digitised values may not fully reflect observed in vivo data.

## Human IV (Intravenous Administration) Model
- In vivo pharmacokinetic data for comparison: 10.1371/journal.pone.0097885


Figure 3. In vivo propranolol plasma concentration versus time profiles after intravenous application in healthy human from the literature (figure 2A control data was used).

  <img width="711" height="351" alt="Screenshot 2025-09-10 at 2 06 48 PM" src="https://github.com/user-attachments/assets/83b672f8-65d8-4171-b4b3-eead4938a100" />

- Source: 10.1371/journal.pone.0097885

Figure 4. In vivo vs predicted time-concentration graph of intravenously administered propranolol to healthy human (in vivo data is in venous plasma concentration, so predicted data was also converted to venous plasma concentration).

<img width="468" height="273" alt="image" src="https://github.com/user-attachments/assets/59f4131f-4722-4d97-82e3-f392feb3212d" />

Table 4. Model performance based on time-concentration profile: Average Absolute Fold Error (AAFE) between predicted and digitised in vivo concentrations in human IV model.

| Metric | Value |
| :------ | ----: |
| AAFE | 1.28 |
| Fraction within 2-fold (0.5–2.0) | 1 |
| Fraction within 3-fold (0.33–3.0) | 1 |

Table 5. Comparison of predicted pharmacokinetic parameters with literature in vivo pharmacokinetic parameters in human IV model

| Metric             |   Predicted | Literature In Vivo |    Pred/Lit |   FE vs Lit | Within 2x (Lit) | Within 3x (Lit) |
| :----------------- | ----------: | -----------------: | ----------: | ----------: | :-------------: | :-------------: |
| AUC₀–∞ (ng·min/mL) | 801.83 |                979 | 0.82 | 1.22 |       TRUE      |       TRUE      |
| CL (mL/min)        | 1247.14 |               1187 | 1.05 | 1.05 |       TRUE      |       TRUE      |
| Vss (L/kg)         | 6.94 |                4.4 |  1.58 |  1.58 |       TRUE      |       TRUE      |
| t½ (min)           |  270.06 |                205 | 1.32 | 1.32 |       TRUE      |       TRUE      |


- Abbreviations: AUC, area under the concentration–time curve; CL, clearance; t½, elimination half-life; Vss, volume of distribution at steady state.

- Note: Human CL reported as total mL/min (70kg standard)

Table 6. Model performance based on PK parameters: Average Absolute Fold Error (AAFE) between predicted and literature in vivo PK parameters in human IV model.

| Metric | Value |
| :------ | ----: |
| AAFE | 1.28 |
| Fraction within 2-fold (0.5–2.0) | 1.0 |
| Fraction within 3-fold (0.33–3.0)| 1.0 |


Note: 
- Only the parameters reported in the literature were calculated and compared.
  - In the referenced study, blood sampling was performed only after the infusion ended. This is also evident because the first sampling time point (5 min) shows the maximum observed concentration - if sampling began during the infusion, the end-of-infusion point (10 min) would be expected to capture Cmax. Because the earliest available sample is at 5 min (no sample at t = 0), the literature Tmax defaults to 5 min by design. Direct comparison of Cmax and Tmax with a simulation that reports concentrations from t = 0 would therefore yield misaligned values that are not physiologically informative. Accordingly, Cmax and Tmax were excluded from subsequent parameter analyses and are not reported in this portfolio.
- The in vivo time–concentration datasets used for Figure 4 and Table 4 were digitised from published figures (as raw time-concentration datasets were unavailable). Digitised data are used only for plotting time-concentration profile and profile-level goodness-of-fit metrics (e.g., AAFE, fold-accuracy). Pharmacokinetic (PK) parameter-level comparisons (Table 5 and 6) are made exclusively against literature PK parameter values, because it is more appropriate to benchmark against actual literature data rather than digitised estimates, as digitised values may not fully reflect observed in vivo data.
  
## Human PO (Oral Administration) Model
- In vivo pharmacokinetic data for comparison: 10.1371/journal.pone.0097885

Figure 5. In vivo propranolol plasma concentration versus time profiles after oral application in healthy human from the literature (figure 2B control data was used).
    <img width="711" height="351" alt="Screenshot 2025-09-10 at 2 06 48 PM" src="https://github.com/user-attachments/assets/83b672f8-65d8-4171-b4b3-eead4938a100" />

- Source: 10.1371/journal.pone.0097885

  
Figure 6. In vivo vs predicted time-concentration graph of orally administered propranolol to healthy human (in vivo data is in venous plasma concentration, so predicted data was also converted to venous plasma concentration).

<img width="480" height="264" alt="image" src="https://github.com/user-attachments/assets/0b8af275-9950-4c06-a528-feb8bc5836c3" />

Table 7. Model performance based on time-concentration profile: Average Absolute Fold Error (AAFE) between predicted and digitised in vivo concentrations in human PO model.

| Metric                            |       Value |
| :-------------------------------- | ----------: |
| AAFE                              | 1.76 |
| Fraction within 2-fold (0.5–2.0)  | 0.58 |
| Fraction within 3-fold (0.33–3.0) | 0.92 |

Table 8. Comparison of predicted pharmacokinetic parameters with literature in vivo pharmacokinetic parameters in human PO model.

| Metric             |   Predicted | Literature In Vivo |    Pred/Lit |   FE vs Lit | Within 2x (Lit) | Within 3x (Lit) |
| :----------------- | ----------: | -----------------: | ----------: | ----------: | :-------------: | :-------------: |
| Cmax (ng/mL)       | 17.31 |                 28 | 0.62 | 1.62 |       TRUE      |       TRUE      |
| Tmax (min)         |         100 |                180 | 0.56 |         1.8 |       TRUE      |       TRUE      |
| AUC₀–∞ (ng·min/mL) | 11196.36 |               8930 | 1.25 | 1.25 |       TRUE      |       TRUE      |
| t½ (min)           | 270.06 |                214 | 1.26 | 1.26 |       TRUE      |       TRUE      |
| F (%)              | 34.91 |                 27 | 1.29 | 1.29 |       TRUE      |       TRUE      |

- Abbreviations: AUC, area under the concentration–time curve; Cmax, peak concentration; F, oral bioavailability; t½, elimination half-life; Tmax, time point of Cmax.


Table 9. Model performance based on PK parameters: Average Absolute Fold Error (AAFE) between predicted and literature in vivo PK parameters in human PO model.

| Metric | Value |
| :------ | ----: |
| AAFE | 1.43 |
| Fraction within 2-fold (0.5–2.0) | 1.0 |
| Fraction within 3-fold (0.33–3.0)| 1.0 |


Note: 
- Only the parameters reported in the literature were calculated and compared.
- The in vivo time–concentration datasets used for Figure 6 and Table 7 were digitised from published figures (as raw time-concentration datasets were unavailable). Digitised data are used only for plotting time-concentration profile and profile-level goodness-of-fit metrics (e.g., AAFE, fold-accuracy). Pharmacokinetic (PK) parameter-level comparisons (Table 8 and 9) are made exclusively against literature PK parameter values, because it is more appropriate to benchmark against actual literature data rather than digitised estimates, as digitised values may not fully reflect observed in vivo data.
