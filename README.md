># PBPK_Propranolol
Physiologically-based pharmacokinetic (PBPK) modeling of propranolol in rats and humans (IV & PO) using Berkeley Madonna with validation against in vivo data.

## Quickstart (3 steps)
For detailed workflow, refer to [workflow.md](workflow.md)

1) Get the repo  
- Clone: `git clone https://github.com/kimsjjkjn/PBPK_Propranolol && cd PBPK_Propranolol`

2) Run the models (Berkeley Madonna)  
- Open: `code/Rat IV code`, `code/Human IV code`, `code/Human PO code`  
  (On GitHub: open the file ▸ **Raw** ▸ copy all → in Berkeley Madonna: **New** file → paste)  
- Execute: press **Run (▶)** → view results in **Table** → **File ▸ Export Table…** to save CSV  
  - **Human IV uses a 10-min infusion**: The simulation spans (sampling period + 10 min) to include the infusion; for analysis/plots, redefine the time origin at the end of infusion (t′ = t − 10 min). Treat the 10-min concentration as t′ = 0, shift all post-infusion data by −10 min, and discard negative times.

3) See outputs  
- Tables/Figures: `results/` (if empty, open the exported CSVs in Excel and create plots/tables)  
- AAFE calculation (Excel example):  
  - Row-wise FE: `=MAX(pred,obs)/MIN(pred,obs)`  
  - AAFE: `=10^(AVERAGE(ABS(LOG10(FE_range))))`  
- Full result summaries and interpretation: **[docs/results.md](docs/results.md)**, **[docs/discussion.md](docs/discussion.md)**

> Want a quick look without running anything? See **[docs/results.md](docs/results.md)** for the key tables/figures.


# Repository Structure
## workflow/
Detailed workflow of how this project was processed

## code/ 
Berkeley Madonna codes for rat IV, human IV, human PO models
- [Rat IV code](https://github.com/kimsjjkjn/PBPK_Propranolol/blob/main/code/Rat%20IV%20code)
- [Human IV code](https://github.com/kimsjjkjn/PBPK_Propranolol/blob/main/code/Human%20IV%20code)
- [Human PO code](https://github.com/kimsjjkjn/PBPK_Propranolol/blob/main/code/Human%20PO%20code)

## docs/ 
Detailed document of the project
- [Background](docs/background.md)
- [Methods](docs/methods.md)
- [Model Derivation](docs/model_derivation.md)
- [Results](docs/results.md)
- [Discussion](docs/discussion.md)
- [Reflection](docs/reflection.md)
- [References](docs/references.md)
- [Full Document](docs/Full_Document.md) ; all sectiosn merged into one document

# Results Highlight
## Model Performance Summary
**At a glance** · Full results: [docs/Results.md](docs/results.md)


| Model        |        AAFE (Time–Concentration) (digitised) |                          AAFE (PK Parameters) | Key Matches (within 2×)       | Key Mismatches                                                           | Overall Conclusion                                                                                           |
| ------------ | -----------------------: | --------------------------------------------: | ----------------------------- | ------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------ |
| **Rat IV**   |                      1.49 |                1.61 (digitised), 1.31 (literature) | t½, CL, Vss, AUC all within 2× | Slightly high Vss → longer t½                                             | Excellent fit. Exposure (AUC, CL) on target. Reliable and well-validated.                                    |
| **Human IV** | 1.28 | 1.78 (digitised), **2.65 (literature)** | AUC, CL within 2×             | Cmax overpredicted (3×), Tmax mismatch, Vss & t½ strongly overestimated | Partial agreement. Moderate accuracy by 3× rule, but not sufficiently predictive for clinical use.           |
| **Human PO** |                     1.76 |         1.48 (digitised), **1.88 (literature)** | Cmax, Tmax, AUC, F within 2×        | t½ overestimated (~5×)    | Acceptable fit overall. Exposure (AUC, F) well predicted but t½ largely overestimated potentially due to oversimplified absorption model.   |

- Abbreviations: AUC, area under the concentration–time curve; Cmax, peak concentration; CL, clearance; F, oral bioavailability; t½, elimination half-life; Vss, volume of distribution at steady state; Tmax, time point of Cmax.
