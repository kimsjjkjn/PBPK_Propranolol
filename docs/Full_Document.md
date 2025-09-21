# PBPK_Propranolol
Physiologically-based pharmacokinetic (PBPK) modeling of propranolol in rats and humans (IV & PO) using Berkeley Madonna with validation against in vivo data.


# Introduction

## Background

### PBPK
Physiologically based pharmacokinetic (PBPK) modeling is a useful tool for predicting how drugs are absorbed, distributed, metabolized, and excreted (ADME) based on physiological and biochemical factors. Unlike traditional compartmental models, PBPK models use detailed representations of organ-specific blood flows, tissue volumes, and protein binding. This allows for a more realistic simulation of how drugs behave in the body (Rowland et al., 2011).

The main goal of PBPK modeling is to describe and predict drug concentration over time in plasma or blood and tissues under different conditions. This helps estimate important pharmacokinetic parameters such as maximum plasma concentration (Cmax), time to reach Cmax (Tmax), area under the curve (AUC), and half-life (t½). These parameters are crucial for evaluating drug effectiveness and safety (Jones and Yeo, 2013).

Another key use of PBPK modeling is to translate findings from laboratory studies to real-life outcomes, which is known as in vitro–in vivo extrapolation (IVIVE). Data obtained from liver microsomes or hepatocytes, such as intrinsic clearance (CLint) and fraction unbound in plasma (fup) or in blood (fub), can be integrated into PBPK models to predict systemic clearance and bioavailability in humans (Rostami-Hodjegan, 2012). This ability is particularly important in the early stages of drug development, as it reduces the need for extensive or unnecessary animal testing and provides a rational basis for selecting first-in-human (FIH) doses with greater confidence. By running simulations in silico, PBPK models allow researchers to identify and eliminate implausible or unsafe dosing regimens before they are tested experimentally, thereby avoiding wasted resources and minimizing ethical concerns. This approach both saves time in the transition from preclinical to clinical studies and increases the likelihood that FIH doses achieve the desired exposure safely.

Additionally, PBPK models help assess variations between individuals by simulating drug kinetics in populations with different physiological or medical conditions, potentially aiding the development of precision medicines. These may include age, sex, organ impairment, and genetic differences (Jamei et al., 2009). Regulatory agencies like the FDA and EMA now recognize PBPK modeling as a valid method for assessing drug-drug interaction (DDI) risks, predicting outcomes in special populations, and improving clinical trial design (Zhao et al., 2012).

In summary, PBPK modeling offers a structured and connected way to link experimental pharmacology with clinical pharmacokinetics. By providing quantitative predictions of drug behavior in various situations, PBPK has become an essential part of modern drug development and regulatory processes.

### Berkeley Madonna
Berkeley Madonna is a software program specialized in obtaining numerical solutions for models composed of systems of differential equations.

Advantages:
- Very fast computational speed
- Free to use (with some feature limitations)
- Employs an intuitive scripting language, so no advanced programming knowledge is required.

Because all equations must be manually derived, Berkeley Madonna is particularly suitable for beginners in PBPK modeling. It facilitates a clear understanding of the mechanisms behind prediction models and provides a strong foundation in the fundamental concepts of modeling. For this reason, it was chosen as the starting platform for this project, aligning with the learning-oriented objective of building mechanistic insight.

### Propranolol
Propranolol is a non-selective β-blocker that competitively inhibits β1/β2 receptors, lowering heart rate and contractility and thereby myocardial oxygen demand. It is currently used across cardiovascular and non-cardiovascular indications including angina, tachyarrhythmias, hypertension, coronary disease (post-MI benefit), migraine prophylaxis, and essential tremor. It is also commonly used off-label for performance anxiety (Shahrokhi and Gupta, 2023). 

Pharmacokinetically, it undergoes extensive first-pass hepatic metabolism (oral bioavailability is therefore limited) and has a short half-life of about 3 to 6 hours in patients with healthy renal systems (Shahrokhi and Gupta, 2023). 

## Why Propranolol Was Chosen for PBPK Modeling Project
Propranolol was selected as the model compound for this PBPK project primarily because it is extensively studied in clinical pharmacology, providing a rich body of literature data. This allows for robust model validation and makes propranolol an appropriate small-molecule drug to begin with. 



## Project Objectives
- Construct PBPK model of propranolol for healthy rat IV, healthy human IV, and healthy human PO administration.
- Validate the models by comparing simulated concentration–time profiles and resulting parameters against published in vivo pharmacokinetic data.




# Methods

## Software and Workflow
Model development and simulation were performed in Berkeley Madonna (METHOD RK4). Data wrangling and figure generation were done in Excel (digitised literature profiles, PK tables). For the detailed workflow of how this project was processed, please refer to **[Workflow.md](Workflow.md)** in this repository.  


## Model Structure & Assumptions
- A physiologically based, perfusion-limited, well-stirred PBPK model was implemented for rat IV, human IV, and human PO simulations.
- Blood concentrations were the model standard. When literature to be compared reported plasma concentration values, simulated blood concentration values were converted to plasma concentration values at the end using the following equation: `Cp_ve = C_ve / RB` (in case the collected sample is venous blood) or `Cp_ar = C_ar / RB` (in case the collected sample is arterial blood).
- Values of parameters (fup, RB, CL_int, fu_MP, Molecular Weight, etc.) that are needed to construct models were obtained from the literature or SimCYP.
  - *For references of where each parameter used to construct each model was extracted from, refer to Table 1 (rat IV model), 2 (human IV model) and 3 (human PO model) in '**[docs/Model_Derivation.md](docs/Model_Derivation)**' in 'docs' folder.*
- All equations in PBPK model were manually derived using the basic rationale discussed in the following research paper: https://doi.org/10.2165/00003088-200645050-00006.
  - For derivation of each equation used in model, refer to '**[docs/Model_Derivation.md](docs/Model_Derivation)**' in 'docs' folder.


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

Note: As mentioned above, digitisation can introduce small systematic and random errors, so the dgitised in vivo data may not perfectly reflect the original raw values. Therefore, PK parameter-level evaluation used only literature-reported in vivo PK values. The digitised in vivo time-concentration values were used solely to plot time–concentration profile overlays and compute profile-level metrics (e.g., AAFE, % within 2×/3×), not to derive PK parameters.
    


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



# Discussion
## Rat IV Model
The rat IV model performed well. AAFE was 1.51 for the time–concentration profile and 1.16 for pharmacokinetic (PK) parameters. Major PK parameters (t½, CL, Vss, AUC) were all within 2-fold of literature values. For PK parameter comparisons, only the predicted and literature values were compared, because digitised estimates can deviate from the original in vivo data (digitised data were used only for profile-level metrics as raw time-concentration datasets were unavailable). Accordingly, one should note that because the profile AAFE is computed against digitised values, which can introduce non-trivial error, rather than raw measurements, the “AAFE within 2-fold” finding should be interpreted as approximate rather than exact. Generally, an AAFE within 2-fold is considered good validation for building robust PBPK models (Deepika and Kumar, 2023). Therefore, these results indicate a robust and credible rat IV model.


## Human IV Model
The human IV model showed AAFE 1.28 for the time–concentration profile and 1.28 for PK parameters, with major PK parameters (t½, CL, Vss, AUC) within 2-fold of literature values. PK parameter comparisons use literature-reported values rather than digitised estimates for the same reason as above.

Although Cmax and Tmax were reported in the literature, these two parameters were not included in the comparison. This is because in the cited study, sampling began after the infusion ended. The first available sample (5 min) is the observed maximum, and with no sample at t = 0, Tmax defaults to 5 min by design. Directly contrasting these with simulations that report concentrations from t = 0 would be misaligned and physiologically uninformative. Accordingly, Cmax and Tmax were excluded from parameter analyses.

Overall, the human IV model demonstrates consistent predictive performance within commonly used 2-fold criteria.

## Human PO Model
The human PO model yielded AAFE 1.76 (time–concentration profile) and 1.43 (PK parameters). Major PK parameters (t½, Tmax, Cmax, AUC, F) were all within 2-fold of literature values. As above, parameter comparisons were made against literature rather than digitised estimates. These findings support that the human PO model also provides acceptable predictive accuracy.


# Model Performance Summary

Table 10. PBPK Propranolol – Model Performance Summary.

| Model        |        AAFE (time–concentration) (vs. digitised in vivo) |                          AAFE (PK Parameters) (vs. literature in vivo) | Key Matches (within 2×)       | Key Mismatches                                                           | Overall Conclusion                                                                                           |
| ------------ | -----------------------: | --------------------------------------------: | ----------------------------- | ------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------ |
| **Rat IV**   |                      1.51 |                1.16 | All within 2× | -                                            | Good agreement with in vivo data.                                |
| **Human IV** | 1.28 | 1.28 | All within 2×             | - | Good agreement with in vivo data.           |
| **Human PO** |                     1.76 |         1.43 | All within 2×        | -    |Good agreement with in vivo data.   |

**Note**: The time–concentration AAFE was computed against **digitised values** rather than raw in vivo measurements. Because digitisation can introduce error and does not fully reflect the original datasets, the within-two-fold agreement for the time–concentration profile should be interpreted as **approximate**, not exact.


# Potential Improvement

## Oversimplified Absorption Model (Human PO)
In the human PO model, oral absorption was represented by a single first-order rate constant (ka) without gastric emptying, intestinal transit, or a lag time. However, propranolol’s absorption is influenced by gastric emptying, regional pH, intestinal permeability, and first-pass intestinal metabolism. In other words, the absorption model is oversimplified and does not capture the complexity of in vivo absorption. This simplification primarily affects the early profile (Cmax, Tmax) and bioavailability (F). 

Yet, in PO model results, Cmax, Tmax, AUC, and F are all within 2-fold of the literature, indicating that the simple ka model is coarsely predictive. However, to sufficiently and mechanistically reflect complex mechanism of in vivo absorption in the future, it would be more appropriate to use more complex absorption model rather than this over-simplified model. 

Improvement:
- Use a more mechanistic refinement which would incorporate stomach and intestinal transit compartments (kGE, kT), dynamic intestinal metabolism, and, ultimately, an ACAT-like GI model which accounts for dissolution, solubility, P-gp efflux, and potential enterohepatic recycling to reflect complex nature of absorption in vivo.

# Applications & Future Work
Although this project was originally designed as a proof-of-understanding exercise, the outcomes highlight broader implications for pharmacokinetic modeling in both academic and industrial contexts. 

All models achieved close agreement with in vivo data, demonstrating that a first-principles approach can yield robust predictions when physiological parameters are well-defined. Although these simplest models are good to start with as modeling beginners, more complex factors could be incorporated to better reflect complex mechanisms occuring in actual body (e.g. by integrating enzyme/transporter contributions and refined absorption modules). 

From a translational perspective, this project also illustrates how a learning-oriented PBPK framework can be developed into more practical applications. 

While the current model was intentionally limited in scope, future extensions could support early drug development (for example, by predicting appropriate dosing regimens or informing preclinical-to-clinical scaling strategies), ultimately helping to minimise wasted resources in identifying the optimal dose.

Similarly, the framework could be adapted to simulate other drug compounds or different patient populations such as pediatrics or geriatrics or patients with hepatic impairment, where physiological parameters diverge markedly from healthy adults. In addition, PBPK modeling can be applied to the development of precision medicine, as physiological parameters can be readily modified within the model to predict unique pharmacokinetic behavior in special populations.

These potential directions highlight how even a learning-oriented model can provide a foundation for models with clinical and regulatory impact.


# Reflection
This independent project on physiologically based pharmacokinetic (PBPK) modeling of propranolol was conducted using Berkeley Madonna, with all organ-level differential equations derived from first principles. By constructing and validating healthy rat (IV) and healthy human (IV and PO) models, I developed hands-on experience in mechanistic model building, parameterisation, and quantitative evaluation of model performance.

The project successfully validated the rat IV and human IV and PO models - all three models showed consistent agreement with literature data. While the models are already predictive, the models were quite simplified as it was a first attempt at PBPK modeling. Therefore, future improvements including incorporating gastric emptying and intestinal transit into the oral absorption module and integrating transporter and enzyme dynamics should be done to reflect more complex in vivo mechanism.

Beyond the technical implementation, this project strengthened my understanding of PBPK mechanisms, provided practice in complete ODE derivation, and reinforced systematic model validation using fold-error metrics (FE, AAFE, within 2×/3×).

Overall, this project demonstrates validated, mechanism-based PBPK modeling across species and routes, and also provides a foundation for future extensions toward clinically predictive PBPK modeling.


# References

Brown, R.P., et al., 1997. Physiological parameter values for physiologically based pharmacokinetic models. *Toxicology and Industrial Health*, 13(4), pp.407–484. https://doi.org/10.1177/074823379701300401

Deepika, D. and Kumar, V., 2023. The role of ‘physiologically based pharmacokinetic model (PBPK)’ new approach methodology (NAM) in pharmaceuticals and environmental chemical risk assessment. *International Journal of Environmental Research and Public Health*, 20(4), p.3473. https://doi.org/10.3390/ijerph20043473

DrugBank, 2024. Propranolol. *DrugBank*. Available at: https://go.drugbank.com/drugs/DB00571

Evans, G.H., et al., 2025. The disposition of propranolol. III. Decreased half-life and volume of distribution as a result of plasma binding in man, monkey, dog and rat. *The Journal of Pharmacology and Experimental Therapeutics*, 186(1), pp.114–122. https://doi.org/10.1016/S0022-3565(25)29572-6

Hung, D.Y., et al., 2025. Disposition kinetics of propranolol isomers in the perfused rat liver. *The Journal of Pharmacology and Experimental Therapeutics*, 311(2), pp.822–829. https://doi.org/10.1124/jpet.104.070011

Jamei, M., et al., 2009. Population-based mechanistic prediction of oral drug absorption. *The AAPS Journal*, 11(2), pp.225–237. https://doi.org/10.1208/s12248-009-9099-y

Jones, H.M. and Yeo, K.R., 2013. Basic concepts in physiologically based pharmacokinetic modeling in drug discovery and development. *CPT: Pharmacometrics & Systems Pharmacology*, 2(8), pp.1–12. https://doi.org/10.1038/psp.2013.41

Jones, H.M., et al., 2006. A novel strategy for physiologically based predictions of human pharmacokinetics. *Clinical Pharmacokinetics*, 45(5), pp.511–542. https://doi.org/10.2165/00003088-200645050-00006

Kaufman, D.P., et al., 2023. Physiology, glomerular filtration rate (GFR). *StatPearls*. National Library of Medicine. Available at: https://www.ncbi.nlm.nih.gov/books/NBK500032

Lee, H.B. and Blaufox, M.D., 1985. Blood volume in the rat. *Journal of Nuclear Medicine*, 26(1), pp.72–76. Available at: https://pubmed.ncbi.nlm.nih.gov/3965655

Lee, M., et al., 2022. Prediction of pharmacokinetics of IDP-73152 in humans using physiologically-based pharmacokinetics. *Pharmaceutics*, 14(6), p.1157. https://doi.org/10.3390/pharmaceutics14061157

Mondal, H. and Saran, L., 2024. Hematocrit (HCT). *StatPearls*. National Library of Medicine. Available at: https://www.ncbi.nlm.nih.gov/books/NBK542276

Nicolaï, J., et al., 2015. Verapamil hepatic clearance in four preclinical rat models: towards activity-based scaling. *Biopharmaceutics & Drug Disposition*, 36(7), pp.462–480. https://doi.org/10.1002/bdd.1959

Potter, D., et al., 1969. Character of function and size in kidney during normal growth of rats. *Pediatric Research*, 3(1), pp.51–59. https://doi.org/10.1203/00006450-196901000-00007

Reigner, B., et al., 1989. Comparative pharmacokinetics of propranolol after administration into the portal and systemic circulation in the rat. *Journal of Pharmacology*, 38(2), pp.112–119. https://doi.org/10.1159/000136352

Rostami-Hodjegan, A., 2012. Physiologically based pharmacokinetics joined with in vitro–in vivo extrapolation of ADME: a marriage under the arch of systems pharmacology. *Clinical Pharmacology & Therapeutics*, 92(1), pp.50–61. https://doi.org/10.1038/clpt.2012.65

Rowland, M., et al., 2006. Physiologically based pharmacokinetics in drug development and regulatory science: a workshop report. *Clinical Pharmacokinetics*, 45(5), pp.507–526. https://doi.org/10.2165/00003088-200645050-00006

Rowland, M. and Tozer, T.N., 2011. *Clinical Pharmacokinetics and Pharmacodynamics: Concepts and Applications*. 4th ed. Philadelphia: Wolters Kluwer Health/Lippincott Williams & Wilkins.

Shahrokhi, M. and Gupta, V., 2023. Propranolol. *StatPearls*. National Library of Medicine. Available at: https://www.ncbi.nlm.nih.gov/books/NBK557801/

Shand, D.G., et al., 1972. The disposition of propranolol. *Pharmacology*, 8(4–6), pp.344–352. https://doi.org/10.1159/000136352

Silberx, B.M., et al., 1983. Dose-dependent elimination of propranolol and its major metabolites in humans. *Journal of Pharmaceutical Sciences*, 72(7), pp.725–732. https://doi.org/10.1002/jps.2600720703

Simcyp Simulator, 2023. Version 22. Sheffield, UK: Certara UK Limited.

Singh, K., et al., 1991. Determination of in vivo hepatic extraction ratio from in vitro metabolism by rat hepatocytes. *Drug Metabolism and Disposition*, 19(5), pp.990–996. Available at: https://pubmed.ncbi.nlm.nih.gov/1686248

Taegtmeyer, A.B., et al., 2014. A study of the relationship between serum bile acids and propranolol pharmacokinetics and pharmacodynamics in patients with liver cirrhosis and in healthy controls. *PLOS ONE*, 9(6), pp.e97885–e97885. https://doi.org/10.1371/journal.pone.0097885

Taylor, E.A. and Turner, P., 1981. The distribution of propranolol, pindolol and atenolol between human erythrocytes and plasma. *British Journal of Clinical Pharmacology*, 12(4), pp.543–548. https://doi.org/10.1111/j.1365-2125.1981.tb01263.x

Zhao, P., et al., 2012. Applications of physiologically based pharmacokinetic (PBPK) modeling and simulation during regulatory review. *Clinical Pharmacology & Therapeutics*, 92(1), pp.1–4. https://doi.org/10.1038/clpt.2012.113
