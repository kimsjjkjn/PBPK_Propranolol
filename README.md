# PBPK_Propranolol
Physiologically-based pharmacokinetic (PBPK) modeling of propranolol in rats and humans (IV & PO) using Berkeley Madonna with validation against in vivo data.

## Quickstart (3 steps)
For full workflow, see **[Workflow.md](Workflow.md)**. 

1) Install Berkeley Madonna  
   - Download from the official site for your OS.

2) Run models  
   - Open **Berkeley Madonna → File ▸ New**, paste the code.  
     - Repo codes: `code/Rat IV code`, `code/Human IV code`, `code/Human PO code` (open on GitHub → **Raw** → copy all).  
   - Plot: **Graph ▸ Choose Variables…** → Y = `C_ar` (arterial) or `Cp_ve` (venous plasma). *(Optional)* log-scale Y.

3) See outputs  
   - **Run (▶) → Table → File ▸ Export Table…** (CSV) or copy/paste to Excel.
   - Calculate key PK parameters and metrics (FE & AAFE) and plot Time-Concentration profiles in Excel.
     - For full formulas & PK calculations, see the Excel template in the repository (**[PBPK_Propranolol_Data_Processing.xlsx](PBPK_Propranolol_Data_Processing.xlsx)** )    

> Want a quick look without running anything? See **[docs/Results.md](docs/Results.md)**, **[docs/Discussion.md](docs/Discussion.md)** for the full result summaries and interpretation.


# Repository Structure
## Workflow/
**[Workflow.md](Workflow.md)**: Detailed workflow of how this project was processed

## code/ 
Berkeley Madonna codes for rat IV, human IV, human PO models
- [Rat IV code](https://github.com/kimsjjkjn/PBPK_Propranolol/blob/main/code/Rat%20IV%20code)
- [Human IV code](https://github.com/kimsjjkjn/PBPK_Propranolol/blob/main/code/Human%20IV%20code)
- [Human PO code](https://github.com/kimsjjkjn/PBPK_Propranolol/blob/main/code/Human%20PO%20code)

## docs/ 
Detailed document of the project
- [Background](docs/Background.md) ; What PBPK is, why propranolol was chosen, and the project’s objective.
- [Methods](docs/Methods.md) ; Software, datasets, parameter sources, model structure, and evaluation metrics (FE/AAFE, PK).
- [Model Derivation](docs/model_derivation.md) ; Derivation of core ODEs/equations used to construct each model, key assumptions, blood↔plasma conversions, and Kp estimation approach.
- [Results](docs/Results.md) ; Side-by-side comparison of in vivo data and model predictions (IV/PO; rat/human), with AAFE and within-2×/3× metrics.
- [Discussion](docs/Discussion.md) ; Evaluation of validity of models, interpretation of fits/mismatches (e.g., Vss, t½, Cmax), limitations, and improvement ideas.
- [Reflection](docs/Reflection.md) ; Lessons learned, modeling choices/trade-offs, and next steps from a student perspective.
- [References](docs/References.md) ; Full citations for all literature used.
- [Full Document](docs/Full_Document.md) ; All sections merged into a single page for continuous reading/printing, excep for [Model Derivation](docs/model_derivation.md) section.

# Key Results Highlight
## Model Performance Summary
**At a glance** · Full results: [docs/Results.md](docs/Results.md)


| Model        |        AAFE (Time–Concentration) (digitised) |                          AAFE (PK Parameters) | Key Matches (within 2×)       | Key Mismatches                                                           | Overall Conclusion                                                                                           |
| ------------ | -----------------------: | --------------------------------------------: | ----------------------------- | ------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------ |
| **Rat IV**   |                      1.49 |                1.61 (digitised), 1.31 (literature) | t½, CL, Vss, AUC all within 2× | Slightly high Vss → longer t½                                             | Excellent fit. Exposure (AUC, CL) on target. Reliable and well-validated.                                    |
| **Human IV** | 1.28 | 1.78 (digitised), **2.65 (literature)** | AUC, CL within 2×             | Cmax overpredicted (3×), Tmax mismatch, Vss & t½ strongly overestimated | Partial agreement. Moderate accuracy by 3× rule, but not sufficiently predictive for clinical use.           |
| **Human PO** |                     1.76 |         1.48 (digitised), **1.88 (literature)** | Cmax, Tmax, AUC, F within 2×        | t½ overestimated (~5×)    | Acceptable fit overall. Exposure (AUC, F) well predicted but t½ largely overestimated potentially due to oversimplified absorption model.   |

- Abbreviations: AUC, area under the concentration–time curve; Cmax, peak concentration; CL, clearance; F, oral bioavailability; t½, elimination half-life; Vss, volume of distribution at steady state; Tmax, time point of Cmax.
