# PBPK_Propranolol
Physiologically-based pharmacokinetic (PBPK) modeling of propranolol in rats and humans (IV & PO) using Berkeley Madonna with validation against in vivo data.

# What this repository is
This repository is a learning-oriented, proof-of-understanding portfolio designed to demonstrate my ability to derive ODE-based PBPK models from first principles and to critically evaluate discrepancies.
It emphasizes first-principles derivation (to strengthen understanding of the mechanisms behind PBPK modeling), explicit documentation of assumptions, and transparent, reproducible validation of key metrics (AAFE, FE, Within 2×/3×). Simulations were performed in Berkeley Madonna, while all validation and metric calculations are reproduced transparently in Excel using formulas (please refer to **[PBPK_Propranolol_Data_Processing.xlsx](PBPK_Propranolol_Data_Processing.xlsx)** in this repository).


# License
Code under MIT (**[MIT_License](/License/MIT_License)**), docs/figures under CC BY 4.0 (**[License-DOCS](/License/License-DOCS)**).


# Quickstart (3 steps)
For full workflow, see **[Workflow.md](Workflow.md)**. 

1) Install Berkeley Madonna  
   - Download from the official site (https://berkeley-madonna.myshopify.com/pages/download).

2) Run models  
   - Open **Berkeley Madonna → File ▸ New**, paste the code.  
     - Repo codes: [Rat IV code](https://github.com/kimsjjkjn/PBPK_Propranolol/blob/main/code/Rat%20IV%20code), [Human IV code](https://github.com/kimsjjkjn/PBPK_Propranolol/blob/main/code/Human%20IV%20code), [Human PO code](https://github.com/kimsjjkjn/PBPK_Propranolol/blob/main/code/Human%20PO%20code) (open on GitHub → **Raw** → copy all).  
   - Plot: **Graph ▸ Choose Variables…** → Y = `C_ar` (arterial) or `Cp_ve` (venous plasma).
     - The Y-axis selected in the model should correspond to the Y-axis reported in the literature for comparison. For example, if the literature presents venous plasma concentration on the Y-axis, the model should use the same.  
     - *(Optional)* log-scale Y.
   - See outputs: **Run (▶) → Table → File ▸ Export Table…** (CSV) or copy/paste to Excel.

3) Calculation & Validation
   - Calculate key Pharmacokinetic (PK) parameters and metrics (FE & AAFE) and plot time-concentration profiles in Excel.
     - For full formulas for PK parameter and metric calculations, see the Excel file in the repository (**[PBPK_Propranolol_Data_Processing.xlsx](PBPK_Propranolol_Data_Processing.xlsx)** )    

> Want a quick look without running anything? See **[docs/Results.md](docs/Results.md)**, **[docs/Discussion.md](docs/Discussion.md)** for the full result summaries and interpretation.


# Repository Structure
## Workflow.md
**[Workflow.md](Workflow.md)**: Detailed workflow of how this project was processed

## code/ 
Berkeley Madonna codes for rat IV, human IV, human PO models
- [Rat IV code](https://github.com/kimsjjkjn/PBPK_Propranolol/blob/main/code/Rat%20IV%20code)
- [Human IV code](https://github.com/kimsjjkjn/PBPK_Propranolol/blob/main/code/Human%20IV%20code)
- [Human PO code](https://github.com/kimsjjkjn/PBPK_Propranolol/blob/main/code/Human%20PO%20code)

## PBPK_Propranolol_Data_Processing.xlsx 
**[PBPK_Propranolol_Data_Processing.xlsx](PBPK_Propranolol_Data_Processing.xlsx)**: Excel workbook for processing PK data: computes key PK parameters, Fold Error (FE), and AAFE, and generates time–concentration plots via embedded formulas.

## docs/ 
Detailed document of the project
- **[Introduction](docs/Introduction.md)** ; What PBPK is, why Berkeley Madonna was chosen, what propranolol is, why propranolol was chosen, and the project’s objective.
- **[Methods](docs/Methods.md)** ; Software, datasets, parameter sources, model structure, and evaluation metrics (FE/AAFE, PK).
- **[Model Derivation](docs/Model_Derivation.md)** ; Derivation of core ODEs/equations used to construct each model.
- **[Results](docs/Results.md)** ; Side-by-side comparison of in vivo data and model predictions (IV/PO; rat/human), with AAFE and within-2×/3× metrics.
- **[Discussion](docs/Discussion.md)** ; Evaluation of validity of models, improvement ideas, application and future work.
- **[Reflection](docs/Reflection.md)** ; Lessons learned and next steps from a student perspective.
- **[References](docs/References.md)** ; Full Harvard style citations for all literature used.
- **[Full Document](docs/Full_Document.md)** ; All sections merged into a single page for continuous reading/printing, except for [Model Derivation](docs/Model_Derivation.md) section.

# Key Results Highlight
**At a glance** · Full results: [docs/Results.md](docs/Results.md)

Figure 2. **In vivo vs predicted time-concentration graph of intravenously administered propranolol to healthy rat.**

<img width="468" height="273" alt="image" src="https://github.com/user-attachments/assets/a00ee682-a03b-4217-a0af-4c3cdd854fb2" />

Figure 4. **In vivo vs predicted time-concentration graph of intravenously administered propranolol to healthy human.**

<img width="468" height="273" alt="image" src="https://github.com/user-attachments/assets/9c75ad7b-738e-4f56-b302-1f41b00846a5" />

Figure 6. **In vivo vs predicted time-concentration graph of orally administered propranolol to healthy human.**

  <img width="468" height="273" alt="image" src="https://github.com/user-attachments/assets/bab10706-535e-49ca-ae34-879d73117815" />

Table 10. **PBPK Propranolol – Model Performance Summary**.

| Model        |        AAFE (time–concentration) (vs. digitised in vivo) |                          AAFE (PK Parameters) (vs. literature in vivo) | Key Matches (within 2×)       | Key Mismatches                                                           | Overall Conclusion                                                                                           |
| ------------ | -----------------------: | --------------------------------------------: | ----------------------------- | ------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------ |
| **Rat IV**   |                      1.51 |                1.16 | All within 2× | -                                            | Good agreement. Reliable and predictive model.                                 |
| **Human IV** | 1.28 | 1.28 | All within 2×             | - | Good agreement. Reliable and predictive model.           |
| **Human PO** |                     1.76 |         1.43 | All within 2×        | -    |Good agreement. Reliable and predictive model.   |

**Note**: The time–concentration AAFE was computed against **digitised values** rather than raw in vivo measurements. Because digitisation can introduce error and does not fully reflect the original datasets, the within-two-fold agreement for the time–concentration profile should be interpreted as **approximate**, not exact.
