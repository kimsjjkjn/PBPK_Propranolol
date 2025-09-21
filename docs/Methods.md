# Methods

## Software and Workflow
Model development and simulation were performed in Berkeley Madonna (METHOD RK4). Data wrangling and figure generation were done in Excel (digitised literature profiles, PK tables). For the detailed workflow of how this project was processed, please refer to **[Workflow.md](Workflow.md)** in this repository.  


## Model Structure & Assumptions
- A physiologically based, perfusion-limited, well-stirred PBPK model was implemented for rat IV, human IV, and human PO simulations.
- Blood concentrations were the model standard. When literature to be compared reported plasma concentration values, simulated blood concentration values were converted to plasma concentration values at the end using the following equation: `Cp_ve = C_ve / RB` (in case the collected sample is venous blood) or `Cp_ar = C_ar / RB` (in case the collected sample is arterial blood).
- All equations in PBPK model were manually derived using the basic rationale discussed in the following research paper: https://doi.org/10.2165/00003088-200645050-00006. 
- Values of parameters (fup, RB, CL_int, fu_MP, Molecular Weight, etc.) were obtained from the literature or SimCYP.
  - MW, pKa, logP, fup, RB were drug-specific properties (constant in rat and human models),
  - whilst physiological parameters such as organ volumes/flows, cardiac output, hematocrit, etc. were species-specific parameters (different in rat and human models).
  - *For references of where each parameter was extracted from, refer to 'Table 1. Parameters obtained from literature that are used to construct rat IV model and their references' in '**[docs/Model_Derivation.md](docs/Model_Derivation)**' in 'docs' folder.*
- Kp (tissue-to-plasma partition coefficient) values were obtained in Excel using standard partition coefficient calculators (Poulin–Theil):


  <img width="578" height="327" alt="Screenshot 2025-09-15 at 1 51 55 PM" src="https://github.com/user-attachments/assets/1d280f9c-fe0e-4fa4-8c0f-007078901cff" />

- For derivation of each equation used in model, refer to '**[docs/Model_Derivation.md](docs/Model_Derivation)**' in 'docs' folder.

## Data & Validation
- After completing simulations in Berkeley Madonna, the raw time-concentration datasets were exported to Excel.
- The in-vivo Time-Concentration values were digitised from published figures (as raw datasets were unavailable). Digitisation can introduce small systematic and random errors, so the “Digitised In-Vivo” numbers may not perfectly reflect the original raw values, as also demonstrated in the **Results** section). 
- Simulated and digitised in vivo datasets were overlaid in the same graph in Excel for direct comparison of Time-Concentration profiles.  
- Model performance based on Time-Concentration profile was evaluated by Average Absolute Fold Error (AAFE) and % within 2-fold / 3-fold error ranges (adopted from the following research paper: [https://doi.org/10.2165/00003088-200645050-00006](https://doi.org/10.3390/pharmaceutics14061157)):

   <img width="631" height="291" alt="Screenshot 2025-09-10 at 10 29 07 PM" src="https://github.com/user-attachments/assets/799af2d3-9e5e-4f78-bbb7-2e261a5cb61f" />

  - Note: Because raw Time-Concentration datasets were not provided by original literature, digitised In Vivo data were used to plot graph and evaluate overall model performance. 
- Key PK parameters (Cmax, Tmax, AUC, t½) from the simulated models were calculated and compared with in vivo PK parameters directly reported by reference literature. The evaluation of model performance based on the calculated PK parameters was done by (adopted from the following research paper: https://doi.org/10.2165/00003088-200645050-00006) calculating:
  - Fold error (FE) per parameter = max(predicted, observed) / min(predicted, observed) so FE ≥ 1.0 by definition.
  - Absolute average fold error (AAFE) across parameters = geometric mean of the per-parameter FEs; the paper also reports the % within 2-fold (and 3-fold).
  - Note: As mentioned above, digitisation can introduce small systematic and random errors, so the “Digitised In-Vivo” numbers may not perfectly reflect the original raw values. Accordingly, PK parameter-level evaluation used only literature-reported in-vivo PK values. The digitised in-vivo Time–Concentration values were used solely to plot Time–Concentration profile overlays and compute profile-level metrics (e.g., AAFE, % within 2×/3×), not to derive PK parameters.
    
