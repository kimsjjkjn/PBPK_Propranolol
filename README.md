<img width="347" height="237" alt="image" src="https://github.com/user-attachments/assets/9887d326-1fd9-4a6b-9397-31b6952fc48b" /># PBPK_Propranolol
Physiologically-based pharmacokinetic (PBPK) modeling of propranolol in rats and humans (IV & PO) using Berkeley Madonna with validation against in vivo data.
# Background
## PBPK
Physiologically based pharmacokinetic (PBPK) modeling is a useful tool for predicting how drugs are absorbed, distributed, metabolized, and excreted (ADME) based on physiological and biochemical factors. Unlike traditional compartmental models, PBPK models use detailed representations of organ-specific blood flows, tissue volumes, and protein binding. This allows for a more realistic simulation of how drugs behave in the body (Rowland et al., 2011).

The main goal of PBPK modeling is to describe and predict drug concentration over time in plasma or blood and tissues under different conditions. This helps estimate important pharmacokinetic parameters such as maximum plasma concentration (Cmax), time to reach Cmax (Tmax), area under the curve (AUC), and half-life (t1/2). These parameters are crucial for evaluating drug effectiveness and safety (Jones & Rowland-Yeo, 2013).

Another key use of PBPK modeling is to translate findings from laboratory studies to real-life outcomes, which is known as in vitro–in vivo extrapolation (IVIVE). Data obtained from liver microsomes or hepatocytes, such as intrinsic clearance (CLint) and fraction unbound in plasma (fup) or in blood (fub), can be integrated into PBPK models to predict systemic clearance and bioavailability in humans (Rostami-Hodjegan, 2012). This ability is particularly important in the early stages of drug development, as it reduces the need for extensive or unnecessary animal testing and provides a rational basis for selecting first-in-human (FIH) doses with greater confidence. By running simulations in silico, PBPK models allow researchers to identify and eliminate implausible or unsafe dosing regimens before they are tested experimentally, thereby avoiding wasted resources and minimizing ethical concerns. This approach both saves time in the transition from preclinical to clinical studies and increases the likelihood that FIH doses achieve the desired exposure safely.

Additionally, PBPK models help assess variations between individuals by simulating drug kinetics in populations with different physiological or medical conditions, potentially aiding the development of precision medicines. These may include age, sex, organ impairment, and genetic differences (Jamei, 2009). Regulatory agencies like the FDA and EMA now recognize PBPK modeling as a valid method for assessing drug-drug interaction (DDI) risks, predicting outcomes in special populations, and improving clinical trial design (Zhao et al., 2012).

In summary, PBPK modeling offers a structured and connected way to link experimental pharmacology with clinical pharmacokinetics. By providing quantitative predictions of drug behavior in various situations, PBPK has become an essential part of modern drug development and regulatory processes.

## Why Propranolol Was Chosen for PBPK Modeling
Propranolol was selected as the model compound for this PBPK project primarily because it is extensively studied in clinical pharmacology, providing a rich body of literature data. This allows for robust model validation and makes propranolol an appropriate small-molecule drug to begin with. 


# Objectives
- Construct PBPK model of propranolol for Rat IV, Human IV, and Human PO administration.
- Validate the models by comparing simulated concentration–time profiles and resulting parameters against published in vivo pharmacokinetic data.

# Methods
## Software and Workflow
Model development and simulation were performed in Berkeley Madonna (METHOD RK4). Data wrangling and figure generation were done in Excel (digitised literature profiles, PK tables).
## Model Structure & Assumptions
- A physiologically based, perfusion-limited, well-stirred PBPK model was implemented for rat IV, human IV, and human PO.
- Blood concentrations were the model standard. When literature to be compared reported plasma concentration values, simulated blood concentration values were converted to plasma concentration values at the end using the following equation: Cp_ve = C_ve / RB (in case the collected sample is venous blood) or Cp_ar = C_ar / RB (in case the collected sample is arterial blood).
- All equations in PBPK model were manually derived using the basic rationale discussed in the following research paper: Jones, Hannah M, et al. “A Novel Strategy for Physiologically Based Predictions of Human Pharmacokinetics.” Clinical Pharmacokinetics, vol. 45, no. 5, 2006, pp. 511–542, https://doi.org/10.2165/00003088-200645050-00006. 
- Values of parameters (fup, RB, CL_int, fu_MP, Molecular Weight, etc.) were obtained from the literature or SimCYP. MW, pKa, logP, fup, RB were drug-specific properties (constant in rat and human models), whilst physiological parameters such as organ volumes/flows, cardiac output, hematocrit, etc. were species-specific parameters (different in rat and human models).
- Kp values were obtained in Excel using standard partition coefficient calculators (Poulin–Theil): <img width="249" height="94" alt="Screenshot 2025-09-10 at 1 41 10 PM" src="https://github.com/user-attachments/assets/4ea4e765-38f3-433e-b0a3-bcd3b51a770e" />
- For derivation of each equation used in model, refer to 'docs' section.
## Data & Validation
- After completing simulations in Berkeley Madonna, the raw time-concentration datasets were exported to Excel.
- The in-vivo Time-Concentration values were digitised from published figures (raw datasets were unavailable). Digitisation can introduce small systematic and random errors, so the “Digitised In-Vivo” numbers may not perfectly reflect the original raw values. 
- Simulated and digitised in vivo datasets were overlaid in Excel for direct comparison.  
- Model performance based on concentration-time profile was evaluated by Average Absolute Fold Error (AAFE) and % within 2-fold / 3-fold error ranges:

   <img width="631" height="291" alt="Screenshot 2025-09-10 at 10 29 07 PM" src="https://github.com/user-attachments/assets/799af2d3-9e5e-4f78-bbb7-2e261a5cb61f" />

  - Note: Because raw time-concentration datasets were not provided by original literature, digitised In Vivo data were used to plot graph and evaluate overall model performance. 
- Where available, key PK parameters (Cmax, Tmax, AUC, t1/2) were extracted and compared. The evaluation of model performance based on the calculated PK parameters was done by (adopted from the following research paper: https://doi.org/10.2165/00003088-200645050-00006) calculating:
  - Fold error (FE) per parameter = max(predicted, observed) / min(predicted, observed) so FE ≥ 1.0 by definition.
  - Average-fold error (AFE/AAFE) across parameters = geometric mean of the per-parameter FEs; the paper also reports the % within 2-fold (and 3-fold).
  - Note: As mentioned above, digitisation can introduce small systematic and random errors, so the “Digitised In-Vivo” numbers may not perfectly reflect the original raw values. Therefore both digitised In Vivo parameter values and In Vivo parameter values directly reported by the literature were used to evaluate overall the model performance based on parameters calculated.
    
# Results
## Rat IV Model
- in vivo pharmacokinetic data for comparison: doi.org/10.1159/000136352
- Figure 1. Rat IV: In Vivo figure (figure 1 control data was used).
  <img width="616" height="496" alt="Screenshot 2025-09-10 at 3 13 19 PM" src="https://github.com/user-attachments/assets/e821a4a7-fc80-422e-940d-2287ed015a3b" />

- Figure 2. Rat IV: Simulated vs Digitised In Vivo Propranolol Blood Concentrations.
<img width="347" height="237" alt="image" src="https://github.com/user-attachments/assets/39e252f2-65f1-4d8d-8272-1288711b2b2c" />

- Table 1. Model performance based on concentration–time profile: Average Absolute Fold Error (AAFE) between Predicted and In Vivo concentrations in the IV rat model
  
| Metric | Value |
| :------ | ----: |
| AAFE | 1.491919857 |
| Fraction within 2-fold (0.5–2.0) | 1 |
| Fraction within 3-fold (0.33–3.0) | 1 |

- Table 2. Comparison of Predicted Pharmacokinetic Parameters with Digitised and literature In Vivo Pharmacokinetic Parameters in IV Rat Model

| Parameter            | Predicted (model) | Digitised In Vivo | Literature In Vivo | Pred/Dig | FE vs Dig | Within 2× (Dig) | Within 3× (Dig) | Pred/Lit | FE vs Lit | Within 2× (Lit) | Within 3× (Lit) |
|----------------------|------------------:|------------------:|-------------------:|---------:|----------:|:----------------:|:----------------:|---------:|----------:|:---------------:|:---------------:|
| AUC∞ (ng·min/mL)     | 28,349            | 24,850            | 27,122             | 1.14     | 1.14      | True             | True             | 1.05     | 1.05      | True            | True            |
| CL (mL/kg/min)       | 88.2              | 100.6             | 92.2               | 0.88     | 1.14      | True             | True             | 0.96     | 1.05      | True            | True            |
| Vd (L/kg)            | 8.64              | 5.63              | 5.30               | 1.53     | 1.53      | True             | True             | 1.63     | 1.63      | True            | True            |
| t½ (min)             | 67.9              | 38.8              | 40                 | 1.75     | 1.75      | True             | True             | 1.70     | 1.70      | True            | True            |


Route-level summary (Rat IV)					
- vs Digitised: AAFE = 1.37, within 2× = 100%, within 3× = 100%.
- vs Literature: AAFE = 1.32, within 2× = 100%, within 3× = 100%.

Note: The in vivo data were digitised from published figures rather than obtained from raw datasets as they were unavailable; therefore, they may not perfectly reflect the original raw values as shown in table 2. 

## Human IV Model
- in vivo pharmacokinetic data for comparison: 10.1371/journal.pone.0097885
- Figure 3. Human IV: In Vivo figure (figure 2A control data was used)
  <img width="711" height="351" alt="Screenshot 2025-09-10 at 2 06 48 PM" src="https://github.com/user-attachments/assets/83b672f8-65d8-4171-b4b3-eead4938a100" />
- Figure 4. Human IV: Simulated vs Digitised In Vivo Propranolol Plasma Concentrations (in vivo data is in venous plasma concentration, so simulated data was also converted to venous plasma concentration).

<img width="446" height="278" alt="image" src="https://github.com/user-attachments/assets/c09201b8-198a-4f61-906d-f91a04424ebf" />

- Table 3. Model performance based on concentration–time profile: Average Absolute Fold Error (AAFE) between Predicted and In Vivo concentrations in the IV human model

| Metric | Value |
| :------ | ----: |
| AAFE | 1.278428459 |
| Fraction within 2-fold (0.5–2.0) | 1 |
| Fraction within 3-fold (0.33–3.0) | 1 |

- Table 4. Comparison of Predicted Pharmacokinetic Parameters with Digitised and literature In Vivo Pharmacokinetic Parameters in IV Human Model

| Human IV                  | Predicted   | Digitised In Vivo | Literature In Vivo | Pred/Dig   | FE vs Dig | Within 2× (Dig) | Within 3× (Dig) | Pred/Lit   | FE vs Lit | Within 2× (Lit) | Within 3× (Lit) |
|----------------------------|-------------|-------------------|--------------------|------------|-----------|-----------------|-----------------|------------|-----------|-----------------|-----------------|
| Cmax (ng/mL)              | 34.54493085 | 8                 | 12.3               | 4.318116356| 4.318116356| FALSE           | FALSE           | 2.808530963| 2.808530963| FALSE           | TRUE            |
| Tmax (min)                | 0           | 5                 | 5                  | 0          | ∞         | FALSE           | FALSE           | 0          | ∞         | FALSE           | FALSE           |
| AUC₀–∞ (ng·min/mL)        | 801.8329383 | 591.1275773       | 979                | 1.356446508| 1.356446508| TRUE            | TRUE            | 0.819032623| 1.220952587| TRUE            | TRUE            |
| CL (mL/min)               | 1,247.14    | 1,691.68          | 1187               | 0.737220372| 1.356446508| TRUE            | TRUE            | 1.050667718| 1.050667718| TRUE            | TRUE            |
| Vd (L/kg)                 | 29.12554313 | 22.6293637        | 4.4                | 1.287068586| 1.287068586| TRUE            | TRUE            | 6.61944162 | 6.61944162 | FALSE           | FALSE           |
| t½ (min)                  | 1133.134406 | 649.0483707       | 205                | 1.745839689| 1.745839689| TRUE            | TRUE            | 5.527484906| 5.527484906| FALSE           | FALSE           |


- Note: Human CL reported as total mL/min (70kg standard)

Route-level summary (IV)
- vs Digitised (excluding IV Tmax, which is 0 by definition): AAFE = 1.78, within 2× = 80%, within 3× = 80%
- vs Literature (excluding IV Tmax): AAFE = 2.65, within 2× = 40%, within 3× = 60%

Note: The in vivo data were digitised from published figures rather than obtained from raw datasets as they were unavailable; therefore, they may not perfectly reflect the original raw values as shown in table 4. 

## Human PO Model
- in vivo pharmacokinetic data for comparison: 10.1371/journal.pone.0097885
- Figure 5. Human PO: In Vivo figure (figure 2B control data was used)
    <img width="711" height="351" alt="Screenshot 2025-09-10 at 2 06 48 PM" src="https://github.com/user-attachments/assets/83b672f8-65d8-4171-b4b3-eead4938a100" />
- Figure 6. Human PO: Simulated vs Digitised In Vivo Propranolol Plasma Concentrations (in vivo data is in venous plasma concentration, so simulated data was also converted to venous plasma concentration).
  <img width="361" height="217" alt="image" src="https://github.com/user-attachments/assets/ad72b1e4-84d7-46be-b58a-e0a33a8ab9fc" />
- Table 5. Model performance based on concentration–time profile: Average Absolute Fold Error (AAFE) between Predicted and In Vivo concentrations in the PO human model

| Metric                            |       Value |
| :-------------------------------- | ----------: |
| AAFE                              | 1.758673167 |
| Fraction within 2-fold (0.5–2.0)  | 0.583333333 |
| Fraction within 3-fold (0.33–3.0) | 0.916666667 |

- Table 6. Comparison of Predicted Pharmacokinetic Parameters with Digitised and literature In Vivo Pharmacokinetic Parameters in PO Human Model

| Human PO                  | Predicted   | Digitised In Vivo | Literature In Vivo | Pred/Dig    | FE vs Dig   | Within 2× (Dig) | Within 3× (Dig) | Pred/Lit    | FE vs Lit   | Within 2× (Lit) | Within 3× (Lit) |
|----------------------------|-------------|-------------------|--------------------|-------------|-------------|-----------------|-----------------|-------------|-------------|-----------------|-----------------|
| Cmax (ng/mL)              | 17.31471324 | 20                | 28                 | 0.865735662 | 1.15508699  | TRUE            | TRUE            | 0.618382616 | 1.617121786 | TRUE            | TRUE            |
| Tmax (min)                | 100         | 60                | 180                | 1.666666667 | 1.666666667 | TRUE            | TRUE            | 0.555555556 | 1.8         | TRUE            | TRUE            |
| AUC₀–∞ (ng·min/mL)        | 11196.36484 | 6967.874838       | 8930               | 1.606855045 | 1.606855045 | TRUE            | TRUE            | 1.253792255 | 1.253792255 | TRUE            | TRUE            |
| t½ (min)                  | 1055.749924 | 538.488155        | 214                | 1.960581516 | 1.960581516 | TRUE            | TRUE            | 4.933410858 | 4.933410858 | FALSE           | FALSE           |
| F (%)                     | 34.90865834 | 29.46857457       | 27                 | 1.184606274 | 1.184606274 | TRUE            | TRUE            | 1.292913272 | 1.292913272 | TRUE            | TRUE            |


Route-level summary (PO)
- vs Digitised: AAFE = 1.483473576, within 2× = 80%, within 3× = 100%
- vs Literature (for the parameters reported in the paper: Cmax, Tmax, AUC, t½, F): AAFE = 1.876685502, within 2× = 80%, within 3× = 80%


Note: The in vivo data were digitised from published figures rather than obtained from raw datasets as they were unavailable; therefore, they may not perfectly reflect the original raw values as shown in table 6. 

# Discussion
## Rat IV Model
The rat IV model showed excellent performance, with an AAFE of 1.5 based on the time–concentration profile and an AAFE of around 1.3 based on the PK parameters (both digitised and literature in vivo data). All major pharmacokinetic parameters (t½, CL, Vd, AUC) were predicted within 2-fold of both digitised and literature values. Generally, an AAFE within 2-fold is considered good validation for building robust PBPK models (Deepika et al., 2023). Therefore, this result indicates that the constructed rat IV model is reliable and well validated.

## Human IV Model
Although the comparison with digitised in vivo data yielded an AAFE of 1.21 based on the time–concentration profile and 1.74 based on PK parameters, comparison with literature values gave a higher AAFE of 2.73. It is generally more appropriate to benchmark against actual literature data rather than digitised estimates, as digitised values may not fully reflect observed in vivo data (except where digitisation is unavoidable, such as for time–concentration profiles). Prediction error within 3-fold is widely accepted as informative but less reliable than within 2-fold; it is often regarded as moderate accuracy, sometimes acceptable for screening or early development, but usually insufficient for confident clinical application. Therefore, the AAFE of 2.73 based on PK parameters when compared with literature indicates that the model is not reliably predictive in humans. More specifically, while AUC and CL were reproduced reasonably well (within 2-fold), other key parameters including Cmax, Tmax, Vd, and t½ showed large discrepancies (e.g., Cmax was overpredicted by 3–4 fold). In particular, the overestimation of Vd and t½ suggests that human IV pharmacokinetics were not adequately captured. Thus, although the human IV model shows partial agreement, it is not clinically predictive.


## Human PO Model
The human PO model showed an AAFE of 1.74 based on the time–concentration profile and 1.4 based on PK parameters when compared with digitised data. However, when compared with literature values, the AAFE increased to 2.0. As with the IV case, comparison with literature data is more meaningful. An AAFE near 2 sits at the boundary of commonly accepted accuracy (i.e., many studies consider ≤2-fold acceptable) (Deepika et al., 2023). More specifically, while some parameters such as Cmax, AUC, and F were well predicted (within 2-fold), others such as Tmax and t½ were not well captured (Tmax was predicted to be 3.6-fold faster, and t½ overestimated by more than 5-fold). This discrepancy likely reflects limitations of the absorption model, which did not account for processes such as intestinal secretion and reabsorption. Therefore, although the human PO model demonstrates acceptable prediction and partial agreement for certain parameters, it is not sufficiently predictive for clinical application.


# Model Performance Summary

- Table 7. PBPK Propranolol – Model Performance Summary

| Model        |        AAFE (Time–Concentration) (digitised) |                          AAFE (PK Parameters) | Key Matches (within 2×)       | Key Mismatches                                                           | Overall Conclusion                                                                                           |
| ------------ | -----------------------: | --------------------------------------------: | ----------------------------- | ------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------ |
| **Rat IV**   |                      1.5 |                \~1.3 (digitised & literature) | t½, CL, Vd, AUC all within 2× | Slightly high Vd → longer t½                                             | Excellent fit. Exposure (AUC, CL) on target. Reliable and well-validated.                                    |
| **Human IV** | 1.21 | 1.74 (digitised PK), **2.73 (literature PK)** | AUC, CL within 2×             | Cmax overpredicted (3–4×), Tmax mismatch, Vd & t½ strongly overestimated | Partial agreement. Moderate accuracy by 3× rule, but not sufficiently predictive for clinical use.           |
| **Human PO** |                     1.74 |         1.4 (digitised), **2.0 (literature)** | Cmax, AUC, F within 2×        | Tmax too fast (3.6×), t½ overestimated (>5×)                             | Acceptable prediction for exposure, but absorption model too simple. Not sufficiently predictive clinically. |

## Key Takeaways
### Validated IV models
- Rat IV and Human IV reproduce systemic exposure (AUC, CL) reasonably, but Human IV overestimates Vd and t½.
### Human Oral model
- Human PO captures exposure (AUC, Cmax, F) but misses absorption delays (Tmax) and terminal slope (t½), showing the need for more detailed absorption modeling.


# Potential Reasons for Discrepancies and Solutions
## High Vd and Longer T1/2 (Human IV & PO)
In the human IV and PO models, the terminal half-life (t½) and apparent volume of distribution (Vd) were markedly overestimated. 

Propranolol is a highly lipophilic, basic compound (logP ≈ 3–4, pKa ≈ 9–10). Standard Poulin–Theil Kp equations often overpredict tissue partitioning for such drugs, particularly in adipose, skin, and brain, where binding and lysosomal trapping are exaggerated. This in turn inflates Vd (Vss = ∑Kp·V) and prolongs the terminal slope thus terminal half-life.   

It is rational to question why rat IV fit well while human IV showed discrepancies despite the same drug was modeled. This is due to both species-specific physiology and data resolution. 
- Physiological differences: Rats have a much smaller proportion of adipose and skin tissue relative to body weight. Even if partition coefficients (Kp) are overpredicted, the overall contribution to steady-state volume of distribution (Vss) remains limited.
- Data resolution and sampling: Rat IV studies typically capture concentration–time profiles over a shorter window (hours). This makes any overestimation of the terminal phase less evident. On the other hand, human IV studies extend sampling to 10–12 hours or more, so the prolonged terminal slope from Kp inflation becomes clearly visible in t½ and Vd.

Solution:
- Calculating Kp using equations proposed by Rodgers-Rowland or Schmitt

## Cmax Overprediction (Human IV)
Cmax was overpredicted by ~3–4× the literature value.

The model uses a purely perfusion-limited central compartment. This leads to excessively rapid equilibration and a sharper initial peak than observed. In vivo, propranolol shows arteriovenous concentration gradients and red blood cell binding kinetics, which delay the rise in venous plasma concentrations. Because the observed dataset reflects venous plasma samples, the model’s lack of a shallow mixing phase overpredicts the early concentrations. Additionally, possible variability in plasma protein/RBC partitioning during and immediately after infusion may dampen the peak in clinical data, but this dynamic is not represented in the model.

Solution:
- Maintain infusion dosing but introduce a fast shallow distribution/mixing compartment (e.g., central venous reservoir or permeability-limited lung/heart) to better reflect the delay before drug appears in peripheral venous plasma.

## Tmax Too Early & Terminal Phase Too Long (Human PO)
The oral model predicted Tmax ≈ 50 min vs. 180 min observed, while the terminal slope was prolonged.

Oral absorption was modeled with a single first-order ka, without gastric emptying, intestinal transit, or lag time. However, propranolol’s absorption is known to be influenced by gastric emptying, intestinal permeability, regional pH, and first-pass intestinal metabolism. The fixed FaFg constraint ensured overall bioavailability but could not shape the time profile. Meanwhile, the same distribution issue (inflated Kp) extended the terminal half-life.

Solution:
- Minimal fixes include adding a gastric lag (Tlag) and reducing ka (0.15–0.25 h⁻¹) to align Tmax with observed values. A more mechanistic refinement would incorporate stomach and intestinal transit compartments (kGE, kT), dynamic intestinal metabolism, and, ultimately, an ACAT-like GI model including dissolution, solubility, P-gp efflux, and potential enterohepatic recycling.



# Future Work
- Gastric emptying and transit to be added on PO absorption equations for more realistic and validated 
- These models can be used with variations in parameters to model disease state (e.g. hepatic impairment).

# Reflection
This independent project on physiologically based pharmacokinetic (PBPK) modeling of propranolol was undertaken using Berkeley Madonna, with all organ-level differential equations derived from first principles. Through the construction and validation of rat (IV) and human (IV & PO) models, I gained practical experience in mechanistic model building, parameterisation, and quantitative evaluation of model performance.

The rat IV model achieved high accuracy, with AAFE values around 1.3–1.5 and all major pharmacokinetic parameters (t½, CL, Vd, AUC) predicted within 2-fold of in vivo data, demonstrating reliability of the framework. In contrast, human IV and PO simulations highlighted key limitations: while exposure metrics such as AUC and CL were predicted within 2-fold, discrepancies emerged in parameters like Tmax, Vd, and t½. These issues were traced to simplified absorption modeling and omission of transporter- or enzyme-specific processes. Because it was my first time constructing PBPK model, I started with the simplest model, in the future, absorption model must be developed to reflect more complex real-life absorption mechanism. 

Overall, this project not only established a validated baseline model (rat IV) but also outlined a roadmap for refinement of human models. Future improvements include incorporating gastric emptying and intestinal transit into the oral absorption module, refining hepatic clearance scaling, and integrating transporter and enzyme dynamics. Beyond the technical results, the project provided an opportunity to gain knowledge of the mechanism behind PBPK model, practice complete ODE derivation, systematic model validation using fold-error criteria (FE, AAFE, within 2×/3×), and critical evaluation of mechanistic assumptions.

This exercise reflects both the strengths and challenges of PBPK modeling: while exposure-based predictions can often be achieved with reasonable accuracy, faithfully reproducing shape-dependent parameters such as Tmax and terminal half-life requires deeper biological detail. The project therefore serves as both a validated case study and a platform for future extensions toward clinically predictive PBPK modeling.

# References

https://pmc.ncbi.nlm.nih.gov/articles/PMC9966583/?utm_source=chatgpt.com 

Jamei, M. et al. "Population-based mechanistic prediction of oral drug absorption." The AAPS Journal, vol. 11, no. 2, 2009, pp. 225–237. doi:10.1208/s12248-009-9099-y.

Jones, H. M., and K. Rowland Yeo. "Basic concepts in physiologically based pharmacokinetic modeling in drug discovery and development." CPT: Pharmacometrics & Systems Pharmacology, vol. 2, no. 8, 2013, pp. 1–12. doi:10.1038/psp.2013.41.

Jones, Hannah M, et al. “A Novel Strategy for Physiologically Based Predictions of Human Pharmacokinetics.” Clinical Pharmacokinetics, vol. 45, no. 5, 2006, pp. 511–542, https://doi.org/10.2165/00003088-200645050-00006.

Reigner, B., et al. "Comparative pharmacokinetics of propranolol after administration into the portal and systemic circulation in the rat." Journal of Pharmacology, vol. 38, no. 2, 1989, pp. 112–119. doi:10.1159/000136352.

Rowland, M., et al. "Physiologically based pharmacokinetics in drug development and regulatory science: a workshop report." Clinical Pharmacokinetics, vol. 45, no. 5, 2006, pp. 507–526. doi:10.2165/00003088-200645050-00006.

Rowland, M., and T. N. Tozer. "Clinical Pharmacokinetics and Pharmacodynamics: Concepts and Applications." 4th ed., Wolters Kluwer Health/Lippincott Williams & Wilkins, 2011.

Rostami-Hodjegan, A. "Physiologically based pharmacokinetics joined with in vitro–in vivo extrapolation of ADME: a marriage under the arch of systems pharmacology." Clinical Pharmacology & Therapeutics, vol. 92, no. 1, 2012, pp. 50–61. doi:10.1038/clpt.2012.65.

Taegtmeyer, Anne B, et al. "A Study of the Relationship between Serum Bile Acids and Propranolol Pharmacokinetics and Pharmacodynamics in Patients with Liver Cirrhosis and in Healthy Controls." Vol. 9, no. 6, 6 June 2014, pp. e97885–e97885, https://doi.org/10.1371/journal.pone.0097885.

Zhao, Peng, et al. "Applications of physiologically based pharmacokinetic (PBPK) modeling and simulation during regulatory review." Clinical Pharmacology & Therapeutics, vol. 92, no. 1, 2012, pp. 1–4. doi:10.1038/clpt.2012.113.
