# Methods

## Software and Workflow
Model development and simulation were performed in Berkeley Madonna (METHOD RK4). Data wrangling and figure generation were done in Excel (digitised literature profiles, PK tables).

## Model Structure & Assumptions
- A physiologically based, perfusion-limited, well-stirred PBPK model was implemented for rat IV, human IV, and human PO simulations.
- Blood concentrations were the model standard. When literature to be compared reported plasma concentration values, simulated blood concentration values were converted to plasma concentration values at the end using the following equation: Cp_ve = C_ve / RB (in case the collected sample is venous blood) or Cp_ar = C_ar / RB (in case the collected sample is arterial blood).
- All equations in PBPK model were manually derived using the basic rationale discussed in the following research paper: Jones, Hannah M, et al. “A Novel Strategy for Physiologically Based Predictions of Human Pharmacokinetics.” Clinical Pharmacokinetics, vol. 45, no. 5, 2006, pp. 511–542, https://doi.org/10.2165/00003088-200645050-00006. 
- Values of parameters (fup, RB, CL_int, fu_MP, Molecular Weight, etc.) were obtained from the literature or SimCYP. MW, pKa, logP, fup, RB were drug-specific properties (constant in rat and human models), whilst physiological parameters such as organ volumes/flows, cardiac output, hematocrit, etc. were species-specific parameters (different in rat and human models).
- Kp (tissue-to-plasma partition coefficient) values were obtained in Excel using standard partition coefficient calculators (Poulin–Theil): <img width="249" height="94" alt="Screenshot 2025-09-10 at 1 41 10 PM" src="https://github.com/user-attachments/assets/4ea4e765-38f3-433e-b0a3-bcd3b51a770e" />
- For derivation of each equation used in model, refer to '**[docs/Model_Derivation.md](docs/Model_Derivation)**' section in 'docs' folder.

## Data & Validation
- After completing simulations in Berkeley Madonna, the raw time-concentration datasets were exported to Excel.
- The in-vivo Time-Concentration values were digitised from published figures (raw datasets were unavailable). Digitisation can introduce small systematic and random errors, so the “Digitised In-Vivo” numbers may not perfectly reflect the original raw values. 
- Simulated and digitised in vivo datasets were overlaid in Excel for direct comparison.  
- Model performance based on concentration-time profile was evaluated by Average Absolute Fold Error (AAFE) and % within 2-fold / 3-fold error ranges:

   <img width="631" height="291" alt="Screenshot 2025-09-10 at 10 29 07 PM" src="https://github.com/user-attachments/assets/799af2d3-9e5e-4f78-bbb7-2e261a5cb61f" />

  - Note: Because raw time-concentration datasets were not provided by original literature, digitised In Vivo data were used to plot graph and evaluate overall model performance. 
- Where available, key PK parameters (Cmax, Tmax, AUC, t½) were extracted and compared. The evaluation of model performance based on the calculated PK parameters was done by (adopted from the following research paper: https://doi.org/10.2165/00003088-200645050-00006) calculating:
  - Fold error (FE) per parameter = max(predicted, observed) / min(predicted, observed) so FE ≥ 1.0 by definition.
  - Average-fold error (AFE/AAFE) across parameters = geometric mean of the per-parameter FEs; the paper also reports the % within 2-fold (and 3-fold).
  - Note: As mentioned above, digitisation can introduce small systematic and random errors, so the “Digitised In-Vivo” numbers may not perfectly reflect the original raw values. Therefore both digitised In Vivo parameter values and In Vivo parameter values directly reported by the literature were used to evaluate overall the model performance based on parameters calculated.
    
