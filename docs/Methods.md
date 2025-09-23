# Methods

## Software and Workflow
Model development and simulation were performed in Berkeley Madonna (METHOD RK4). Data wrangling and figure generation were done in Excel (digitised literature profiles, PK tables). For the detailed workflow of how this project was processed, please refer to **[Workflow.md](Workflow.md)** in this repository.  


## Model Structure & Assumptions
- A physiologically based, perfusion-limited, well-stirred PBPK model was implemented for rat IV, human IV, and human PO simulations.
- Blood concentrations were the model standard. When literature to be compared reported plasma concentration values, simulated blood concentration values were converted to plasma concentration values at the end using the following equation: `Cp_ve = C_ve / RB` (in case the collected sample is venous blood) or `Cp_ar = C_ar / RB` (in case the collected sample is arterial blood).
- Values of parameters (fup, RB, CL_int, fu_MP, Molecular Weight, etc.) that are needed to construct models were obtained from the literature or SimCYP.
  - *For references of where each parameter used to construct each model was extracted from, refer to Table 1 (rat IV model), 2 (human IV model) and 3 (human PO model) in '**[docs/Model_Derivation.md](docs/Model_Derivation.md)**' in 'docs' folder.*
- All equations in PBPK model were manually derived using the basic rationale discussed in the following research paper: https://doi.org/10.2165/00003088-200645050-00006.
  - For derivation of each equation used in model, refer to '**[docs/Model_Derivation.md](docs/Model_Derivation.md)**' in 'docs' folder.


## Data & Validation
After completing simulations in Berkeley Madonna, the simulated time-concentration datasets were exported to Excel for data processing and model validation. 

**Time-concentration profiles**
- Note: The in vivo time-concentration values were digitised from published figures, because raw in vivo time-concentration datasets were not provided by original literature. Therefore, digitised in vivo time-concentration datasets were used to plot graphs and evaluate overall model performance based on time-concentration profiles.
    - Digitisation can introduce small systematic and random errors, so the digitised in vivo data may not perfectly reflect the original raw values. 
- Simulated and digitised in vivo datasets were overlaid in the same graph in Excel for direct comparison of time-concentration profiles.  
- Model performance based on time-concentration profile was evaluated by Average Absolute Fold Error (AAFE) and % within 2-fold / 3-fold error ranges (adopted from the following research paper: [https://doi.org/10.2165/00003088-200645050-00006](https://doi.org/10.3390/pharmaceutics14061157)):

   <img width="631" height="291" alt="Screenshot 2025-09-10 at 10 29 07 PM" src="https://github.com/user-attachments/assets/799af2d3-9e5e-4f78-bbb7-2e261a5cb61f" />

**Pharmacokinetic Parameters**
- Key Pharmacokinetic (PK) parameters (Cmax, Tmax, AUC, t½, F, Vss) from the simulated models were calculated and compared with in vivo PK parameters directly reported by reference literature in Excel.
- The evaluation of model performance based on the calculated PK parameters was done by (adopted from the following research paper: https://doi.org/10.2165/00003088-200645050-00006) calculating:
  - Fold error (FE) per parameter = `max(predicted, observed) / min(predicted, observed)` so FE ≥ 1.0 by definition.
  - Absolute average fold error (AAFE) across parameters = geometric mean of the per-parameter FEs; the paper also reports the % within 2-fold (and 3-fold).
  - *For the formulas used to compute each metric and PK parameter, see the Excel file titled **[PBPK_Propranolol_Data_Processing.xlsx](/PBPK_Propranolol_Data_Processing.xlsx)** in this repository - click any relevant cell to view its underlying formula in the formula bar.*

Note: As mentioned above, digitisation can introduce small systematic and random errors, so the digitised in vivo data may not perfectly reflect the original raw values. Therefore, PK parameter-level evaluation used only literature-reported in vivo PK values. The digitised in vivo time-concentration values were used solely to plot time–concentration profile overlays and compute profile-level metrics (e.g., AAFE, % within 2×/3×), not to derive PK parameters.
    
