# Results

## Rat IV Model
- in vivo pharmacokinetic data for comparison: doi.org/10.1159/000136352



Figure 1. Rat IV: In Vivo figure (figure 1 control data was used).


<img width="600" height="800" alt="Screenshot 2025-09-10 at 3 13 19 PM" src="https://github.com/user-attachments/assets/e821a4a7-fc80-422e-940d-2287ed015a3b" />



Figure 2. Rat IV: Simulated vs Digitised In Vivo Propranolol Blood Concentrations.
<img width="468" height="273" alt="image" src="https://github.com/user-attachments/assets/efd3e834-ff4b-4726-8801-47b8a65d2423" />

Table 1. Model performance based on concentration–time profile: Average Absolute Fold Error (AAFE) between Predicted and In Vivo concentrations in the IV rat model
  
| Metric | Value |
| :------ | ----: |
| AAFE | 1.51 |
| Fraction within 2-fold (0.5–2.0) | 1 |
| Fraction within 3-fold (0.33–3.0) | 1 |

Table 2. Comparison of Predicted Pharmacokinetic Parameters with Digitised and literature In Vivo Pharmacokinetic Parameters in IV Rat Model

| Parameter            | Predicted (model) | Digitised In Vivo | Literature In Vivo | Pred/Dig | FE vs Dig | Within 2× (Dig) | Within 3× (Dig) | Pred/Lit | FE vs Lit | Within 2× (Lit) | Within 3× (Lit) |
|----------------------|------------------:|------------------:|-------------------:|---------:|----------:|:----------------:|:----------------:|---------:|----------:|:---------------:|:---------------:|
| AUC₀–∞ (ng·min/mL)     | 30703.66          | 24254.95           | 27122             | 1.27     | 1.27       | True             | True             | 1.13     | 1.13      | True            | True            |
| CL (mL/kg/min)       | 81.42             | 103.07            | 92.2               | 0.79     | 1.27      | True             | True             | 0.88     | 1.13      | True            | True            |
| Vss (L/kg)            | 8.13              | 4.14            | 5.30               | 1.96     | 1.96      | True             | True             | 1.53     | 1.53      | True            | True            |
| t½ (min)             | 69.17              | 27.81              | 40                 | 2.49     | 2.49      | False             | True             | 1.73    | 1.73      | True            | True            |

- Abbreviations: AUC, area under the concentration–time curve; CL, clearance; Vss, volume of distribution at steady state; t½, elimination half-life.

Route-level summary (Rat IV)					
- vs Digitised: AAFE = 1.67, within 2× = 75%, within 3× = 100%.
- vs Literature: AAFE = 1.36, within 2× = 100%, within 3× = 100%.

Note: 
- Only the parameters reported in the literature were calculated and compared.
- The in vivo data were digitised from published figures rather than obtained from raw datasets as they were unavailable; therefore, they may not perfectly reflect the original raw values as shown in table 2. 

## Human IV Model
- in vivo pharmacokinetic data for comparison: 10.1371/journal.pone.0097885


Figure 3. Human IV: In Vivo figure (figure 2A control data was used)
  <img width="711" height="351" alt="Screenshot 2025-09-10 at 2 06 48 PM" src="https://github.com/user-attachments/assets/83b672f8-65d8-4171-b4b3-eead4938a100" />


Figure 4. Human IV: Simulated vs Digitised In Vivo Propranolol Plasma Concentrations (in vivo data is in venous plasma concentration, so simulated data was also converted to venous plasma concentration).

<img width="468" height="273" alt="image" src="https://github.com/user-attachments/assets/efce50cc-c284-4551-8aca-f7192ba1f897" />

Table 3. Model performance based on concentration–time profile: Average Absolute Fold Error (AAFE) between Predicted and In Vivo concentrations in the IV human model

| Metric | Value |
| :------ | ----: |
| AAFE | 1.28 |
| Fraction within 2-fold (0.5–2.0) | 1 |
| Fraction within 3-fold (0.33–3.0) | 1 |

Table 4. Comparison of Predicted Pharmacokinetic Parameters with Digitised and literature In Vivo Pharmacokinetic Parameters in IV Human Model

| Human IV                  | Predicted   | Digitised In Vivo | Literature In Vivo | Pred/Dig   | FE vs Dig | Within 2× (Dig) | Within 3× (Dig) | Pred/Lit   | FE vs Lit | Within 2× (Lit) | Within 3× (Lit) |
|----------------------------|-------------|-------------------|--------------------|------------|-----------|-----------------|-----------------|------------|-----------|-----------------|-----------------|
| Cmax (ng/mL)              | 34.54 | 8                 | 12.3               | 4.32| 4.32| FALSE           | FALSE           | 2.81| 2.81| FALSE           | TRUE            |
| Tmax (min)                | 0           | 5                 | 5                  | 0          | ∞         | FALSE           | FALSE           | 0          | ∞         | FALSE           | FALSE           |
| AUC₀–∞ (ng·min/mL)        | 801.83 | 591.13       | 979                | 1.36| 1.36| TRUE            | TRUE            | 0.82| 1.22| TRUE            | TRUE            |
| CL (mL/min)               | 1,247.14    | 1,691.68          | 1187               | 0.74| 1.36| TRUE            | TRUE            | 1.05| 1.05| TRUE            | TRUE            |
| Vss (L/kg)                 | 29.13 | 22.63        | 4.4                | 1.29| 1.29| TRUE            | TRUE            | 6.62 | 6.62 | FALSE           | FALSE           |
| t½ (min)                  | 1133.13 | 649.05       | 205                | 1.75| 1.75| TRUE            | TRUE            | 5.53| 5.53| FALSE           | FALSE           |

- Abbreviations: AUC, area under the concentration–time curve; Cmax, peak concentration; CL, clearance; t½, elimination half-life; Vss, volume of distribution at steady state; Tmax, time point of Cmax.

- Note: Human CL reported as total mL/min (70kg standard)

Route-level summary (Human IV)
- vs Digitised (excluding IV Tmax, which is 0 by definition): AAFE = 1.78, within 2× = 80%, within 3× = 80%.
- vs Literature (excluding IV Tmax): AAFE = 2.65, within 2× = 40%, within 3× = 60%.

Note: 
- Only the parameters reported in the literature were calculated and compared.
- The in vivo data were digitised from published figures rather than obtained from raw datasets as they were unavailable; therefore, they may not perfectly reflect the original raw values as shown in table 4. 

## Human PO Model
- in vivo pharmacokinetic data for comparison: 10.1371/journal.pone.0097885

Figure 5. Human PO: In Vivo figure (figure 2B control data was used)
    <img width="711" height="351" alt="Screenshot 2025-09-10 at 2 06 48 PM" src="https://github.com/user-attachments/assets/83b672f8-65d8-4171-b4b3-eead4938a100" />

Figure 6. Human PO: Simulated vs Digitised In Vivo Propranolol Plasma Concentrations (in vivo data is in venous plasma concentration, so simulated data was also converted to venous plasma concentration).
  <img width="468" height="273" alt="image" src="https://github.com/user-attachments/assets/ad72b1e4-84d7-46be-b58a-e0a33a8ab9fc" />

Table 5. Model performance based on concentration–time profile: Average Absolute Fold Error (AAFE) between Predicted and In Vivo concentrations in the PO human model

| Metric                            |       Value |
| :-------------------------------- | ----------: |
| AAFE                              | 1.76 |
| Fraction within 2-fold (0.5–2.0)  | 0.58 |
| Fraction within 3-fold (0.33–3.0) | 0.92 |

Table 6. Comparison of Predicted Pharmacokinetic Parameters with Digitised and literature In Vivo Pharmacokinetic Parameters in PO Human Model

| Human PO                  | Predicted   | Digitised In Vivo | Literature In Vivo | Pred/Dig    | FE vs Dig   | Within 2× (Dig) | Within 3× (Dig) | Pred/Lit    | FE vs Lit   | Within 2× (Lit) | Within 3× (Lit) |
|----------------------------|-------------|-------------------|--------------------|-------------|-------------|-----------------|-----------------|-------------|-------------|-----------------|-----------------|
| Cmax (ng/mL)              | 17.31 | 20                | 28                 | 0.87 | 1.16  | TRUE            | TRUE            | 0.62 | 1.62 | TRUE            | TRUE            |
| Tmax (min)                | 100         | 60                | 180                | 1.67 | 1.67 | TRUE            | TRUE            | 0.56 | 1.8         | TRUE            | TRUE            |
| AUC₀–∞ (ng·min/mL)        | 11196.36 | 6967.87       | 8930               | 1.61 | 1.61 | TRUE            | TRUE            | 1.25 | 1.25 | TRUE            | TRUE            |
| t½ (min)                  | 1055.75 | 538.49        | 214                | 1.96 | 1.96 | TRUE            | TRUE            | 4.93 | 4.93 | FALSE           | FALSE           |
| F (%)                     | 34.91 | 29.47       | 27                 | 1.18 | 1.18 | TRUE            | TRUE            | 1.29 | 1.29 | TRUE            | TRUE            |

- Abbreviations: AUC, area under the concentration–time curve; Cmax, peak concentration; F, oral bioavailability; t½, elimination half-life; Tmax, time point of Cmax.


Route-level summary (Human PO)
- vs Digitised: AAFE = 1.48, within 2× = 80%, within 3× = 100%.
- vs Literature: AAFE = 1.88, within 2× = 80%, within 3× = 80%.


Note: 
- Only the parameters reported in the literature were calculated and compared.
- The in vivo data were digitised from published figures rather than obtained from raw datasets as they were unavailable; therefore, they may not perfectly reflect the original raw values as shown in table 6. 
