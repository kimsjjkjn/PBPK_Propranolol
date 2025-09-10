# PBPK_Propranolol
Physiologically-based pharmacokinetic (PBPK) modeling of propranolol in rats and humans (IV &amp; PO) using Berkeley Madonna with validation against in vivo data.
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
Model development and simulation were performed in Berkeley Madonna (METHOD RK4). Data wrangling and figure generation were done in Excel (digitized literature profiles, PK tables).
## Model Structure & Assumptions
- A physiologically based, perfusion-limited, well-stirred PBPK model was implemented for rat IV, human IV, and human PO.
- Blood concentrations were the model standard. When literature to be compared reported plasma values, simulated blood was converted at the end using the following equation: Cp_ve = C_ve / RB.
- All equations in PBPK model were manually derived using the basic rationale discussed in the following research paper (Rowland et al., 2006; DOI: 10.2165/00003088-200645050-00006). 
- Values of parameters (fup, RB, CL_int, fu_MP, Molecular Weight, etc.) were obtained from the literature and SimCYP. MW, pKa, logP, fup, RB were drug-specific properties (constant in rat and human models), whilst physiological parameters such as organ volumes/flows, cardiac output, hematocrit, etc. were species-specific parameters (different in rat and human models).
- Kp values were obtained in Excel using standard partition coefficient calculators (Poulin–Theil): <img width="249" height="94" alt="Screenshot 2025-09-10 at 1 41 10 PM" src="https://github.com/user-attachments/assets/4ea4e765-38f3-433e-b0a3-bcd3b51a770e" />
- For derivation of each equation used in model, refer to 'docs' section.
## Data & Validation
- After completing simulations in Berkeley Madonna, the datasets were exported to Excel.
- Published in vivo concentration–time profiles were digitized from figures (as raw datasets were unavailable).  
- Simulated and in vivo datasets were overlaid in Excel for direct comparison.  
- Model performance was evaluated by Average Absolute Fold Error (AAFE) and % within 2-fold / 3-fold error ranges.
- Where available, key PK parameters (Cmax, Tmax, AUC, t1/2) were extracted and compared.

# Results
## Rat IV Model
- in vivo pharmacokinetic data for comparison: doi.org/10.1159/000136352
- Figure 1. Rat IV: In Vivo figure (figure 1 control data was used).
  <img width="616" height="496" alt="Screenshot 2025-09-10 at 3 13 19 PM" src="https://github.com/user-attachments/assets/e821a4a7-fc80-422e-940d-2287ed015a3b" />

- Figure 2. Rat IV: Simulated vs observed propranolol blood concentrations.
  <img width="619" height="487" alt="Screenshot 2025-09-10 at 1 56 44 PM" src="https://github.com/user-attachments/assets/eaa3857a-8aa9-4e6d-bc54-f16d88571cc7" />
- Table 1. Average Absolute Fold Error (AAFE) between Predicted and In Vivo Concentrations in IV rat model

| Metric | Value |
| :------ | ----: |
| AAFE | 1.491919857 |
| Fraction within 2-fold (0.5–2.0) | 1 |
| Fraction within 3-fold (0.33–3.0) | 1 |

- Table 2. Comparison of literature In Vivo Pharmacokinetic Parameters with Predicted and Digitized In Vivo Pharmacokinetic Parameters in IV rat model

| Metric                   | Predicted (model) | Digitised In Vivo | Literature In Vivo | Pred/Dig | FE vs Dig | Within 2x (Dig) | Pred/Lit | FE vs Lit | Within 2x (Lit) |
|--------------------------|------------------:|------------------:|-------------------:|---------:|----------:|:----------------:|---------:|----------:|:---------------:|
| t½ (min)                 | 67.9              | 38.8              | 40                 | 1.75     | 1.75      | True             | 1.70     | 1.70      | True            |
| CL (mL·kg⁻¹·min⁻¹)       | 88.2              | 100.6             | 92.2               | 0.88     | 1.14      | True             | 0.96     | 1.05      | True            |
| Vd (L·kg⁻¹)              | 8.64              | 5.63              | 5.30               | 1.53     | 1.53      | True             | 1.63     | 1.63      | True            |
| AUC∞ (ng·min·mL⁻¹)       | 28,349            | 24,850            | 27,122             | 1.14     | 1.14      | True             | 1.05     | 1.05      | True            |
 
- Note: The in vivo data were digitized from published figures rather than obtained from raw datasets as they were unavailable; therefore, they may not perfectly reflect the original raw values. 

## Human IV Model
- in vivo pharmacokinetic data for comparison: 10.1371/journal.pone.0097885
- Figure 3. Human IV: In Vivo figure (figure 2A control data was used)
  <img width="711" height="351" alt="Screenshot 2025-09-10 at 2 06 48 PM" src="https://github.com/user-attachments/assets/83b672f8-65d8-4171-b4b3-eead4938a100" />
- Figure 4. Human IV: Simulated vs observed propranolol plasma concentrations (in vivo data is in venous plasma concentration, so simulated data was also converted to venous plasma concentration).
  <img width="362" height="218" alt="image" src="https://github.com/user-attachments/assets/bfd6c49b-5887-46ee-bf1f-150c63581dab" />
- Table 3. Average Absolute Fold Error (AAFE) between Predicted and In Vivo Concentrations in IV human model

| Metric | Value |
| :------ | ----: |
| AAFE | 1.277554836 |
| Fraction within 2-fold (0.5–2.0) | 1 |
| Fraction within 3-fold (0.33–3.0) | 1 |

- Table 4. Comparison of literature In Vivo Pharmacokinetic Parameters with Predicted and Digitized In Vivo Pharmacokinetic Parameters in IV human model

| Metric             | Predicted | Digitised In Vivo | Literature In Vivo | Pred/Dig | FE vs Dig | Within 2x (Dig) | Pred/Lit | FE vs Lit | Within 2x (Lit) |
| :----------------- | --------: | ----------------: | -----------------: | -------: | --------: | :-------------: | -------: | --------: | :-------------: |
| AUC₀–∞ (ng·min/mL) |    712.77 |            616.38 |                979 |    1.156 |     1.156 |       TRUE      |    0.728 |     1.374 |       TRUE      |
| Cmax (ng/mL)       |     7.388 |                 8 |               12.3 |    0.924 |     1.083 |       TRUE      |    0.601 |     1.665 |       TRUE      |
| Tmax (min)         |         0 |                 5 |                  5 |        0 |         – |      FALSE      |        0 |         – |      FALSE      |
| t½ (min)           |    856.01 |            831.18 |                205 |     1.03 |      1.03 |       TRUE      |    4.176 |     4.176 |      FALSE      |

- Note: The in vivo data were digitized from published figures rather than obtained from raw datasets as they were unavailable; therefore, they may not perfectly reflect the original raw values. 

## Human PO Model
- in vivo pharmacokinetic data for comparison: 10.1371/journal.pone.0097885
- Figure 5. Human PO: In Vivo figure (figure 2B control data was used)
    <img width="711" height="351" alt="Screenshot 2025-09-10 at 2 06 48 PM" src="https://github.com/user-attachments/assets/83b672f8-65d8-4171-b4b3-eead4938a100" />
- Figure 6. Human PO: Simulated vs observed propranolol plasma concentrations (in vivo data is in venous plasma concentration, so simulated data was also converted to venous plasma concentration).
  <img width="362" height="217" alt="image" src="https://github.com/user-attachments/assets/7558ae70-f615-4b34-bf5a-e26d52a3312f" />
- Table 5. Average Absolute Fold Error (AAFE) between Predicted and In Vivo Concentrations in PO human model

| Metric                            |       Value |
| :-------------------------------- | ----------: |
| AAFE                              | 1.792876734 |
| Fraction within 2-fold (0.5–2.0)  | 0.666666667 |
| Fraction within 3-fold (0.33–3.0) | 0.916666667 |

- Table 6. Comparison of literature In Vivo Pharmacokinetic Parameters with Predicted and Digitized In Vivo Pharmacokinetic Parameters in PO human model

| Metric             | Predicted | Digitised In Vivo | Literature In Vivo | Pred/Dig | FE vs Dig | Within 2x (Dig) | Pred/Lit | FE vs Lit | Within 2x (Lit) |
| :----------------- | --------: | ----------------: | -----------------: | -------: | --------: | :-------------: | -------: | --------: | :-------------: |
| AUC₀–∞ (ng·min/mL) |  11279.78 |           6984.69 |               8930 |    1.615 |     1.615 |       TRUE      |    1.263 |     1.263 |       TRUE      |
| Cmax (ng/mL)       |     31.31 |                20 |                 28 |    1.566 |     1.566 |       TRUE      |    1.118 |     1.118 |       TRUE      |
| Tmax (min)         |        45 |                60 |                180 |     0.75 |     1.333 |       TRUE      |     0.25 |         4 |      FALSE      |
| t½ (min)           |    1163.5 |            596.76 |                214 |     1.95 |      1.95 |       TRUE      |    5.437 |     5.437 |      FALSE      |
| F (%)              |    39.563 |            28.329 |                 27 |    1.397 |     1.397 |       TRUE      |    1.465 |     1.465 |       TRUE      |

- Note: The in vivo data were digitized from published figures rather than obtained from raw datasets as they were unavailable; therefore, they may not perfectly reflect the original raw values. 

# Discussion
## Rat IV Model
### How Close?
- All four IV metrics are within 2-fold of both the digitised in-vivo values and the literature targets (see “Within 2x” = True across the board).
- AUC∞ is very tight to literature (28,349 vs 27,122 ng·min·mL⁻¹; FE = 1.05, +4.5%) and acceptable vs digitised in-vivo (FE = 1.14).
- CL is close: 88.2 vs 92.2 mL·kg⁻¹·min⁻¹ (FE = 1.05, −4% vs literature; FE = 1.14 vs digitised).
- t½ is long relative to both benchmarks (67.9 min vs 40 / 38.8; FE = 1.70 vs literature, 1.75 vs digitised).
- Vd is high (8.64 vs 5.3 / 5.63 L·kg⁻¹; FE = 1.63 vs literature, 1.53 vs digitised).
- Overall fold accuracy summary: AAFE ≈ 1.32 (vs literature) and ≈ 1.37 (vs digitised) for these four IV endpoints.
### Where it diverges and why
- Half-life and Vd are jointly high. Because t1/2 = 0.693⋅Vd/CL, even a modestly low CL (−4% vs lit) combined with an inflated Vd (≈+63%) naturally yields a longer terminal half-life. Mechanistically this points to:
- Partitioning assumptions (Kp scalars) that over-distribute the drug into tissues (especially adipose/muscle) or an over-estimated fu_p / under-estimated blood-to-plasma ratio (R_b) in the well-stirred framework.
- Terminal-phase slope underestimation (λz too shallow) due to either insufficient weight on the late tail or using points where distribution is not fully complete.
- Exposure (AUC∞) and clearance (CL) are right on target. That suggests the systemic elimination capacity is parameterised reasonably; the main residual bias sits in distributional parameters and λz fitting.
### Interpretation
- From a dose-normalised exposure perspective (AUC∞) the model is essentially calibrated to literature; CL is likewise close. This supports the use of the current elimination parameters for exposure-based predictions.
- The shape of the terminal phase is less accurate (longer tail), driven by an over-large Vd. Until Vd (and thus t1/2) is corrected, the model may over-project late-time concentrations, time-above-threshold, and accumulation on repeated dosing.
### Note
The in-vivo values were digitised from published figures (raw datasets were unavailable). Digitisation can introduce small systematic and random errors, so the “Digitised In-Vivo” numbers may not perfectly reflect the original raw values. We therefore compare to both the digitised points and the literature targets.

## Human IV Model
### How Close?
- Exposure is reasonably aligned. Predicted AUC₀–∞ ≈ 713 ng·min/mL vs in-vivo (digitized) 616 (fold-error, FE ≈ 1.16) and literature 979 (FE ≈ 1.37).
- Cmax 7.39 ng/mL is close to in-vivo 8 (FE ≈ 1.08) and lower than literature 12.3 (FE ≈ 1.67).
- Aggregate accuracy across core exposure metrics (AUC∞, Cmax) is good: AAFE ≈ 1.28; 100% within 2-fold.
### Where it diverges and why
- t½ and Vd are inflated. Predicted t½ ≈ 856 min is similar to in-vivo 831 min (FE ≈ 1.03) but far above literature ≈ 205 min (FE ≈ 4.2). A shallow terminal slope (λz too small) propagates to large Vd (≈ 24.8 L/kg vs literature ≈ 4.4 L/kg) via Vd = CL/λz.
- Tmax = 0 min arises from the model’s instantaneous mixing assumption; clinical sampling typically starts at ≥5 min, so observed Tmax of 5 min is partly a sampling artifact.
### Interpretation
- Early/mid profile (driving AUC, Cmax, CL) is acceptable; CL ≈ 1.40 L/min is within ∼20% of the reported 1.19 L/min.
- The terminal phase is the weak spot. Either (i) the λz window included distribution-phase points, or (ii) distribution parameters (Kp scaling, blood/plasma binding) make elimination appear too slow.
### Note
The in-vivo values were digitised from published figures (raw datasets were unavailable). Digitisation can introduce small systematic and random errors, so the “Digitised In-Vivo” numbers may not perfectly reflect the original raw values. We therefore compare to both the digitised points and the literature targets.

## Human PO Model
### How Close?
- AUC₀–∞ is acceptable: predicted ≈ 11,280 ng·min/mL vs in-vivo 6,985 (FE ≈ 1.62) and literature 8,930 (FE ≈ 1.26).
- Cmax 31.3 ng/mL vs in-vivo 20 (FE ≈ 1.56) and literature 28 (FE ≈ 1.12).
- F ≈ 39.6% vs in-vivo 28.3% (FE ≈ 1.40) and literature 27% (FE ≈ 1.47).
- Tmax 45 min vs in-vivo 60 min (FE ≈ 1.33) and literature 180 min (faster than literature).
- Overall accuracy on the oral set (AUC∞, Cmax, F): AAFE ≈ 1.79; 67% within 2-fold, 92% within 3-fold.
### Where it diverges and why
- The absorption equation does not reflect secretion or reabsorption. Consequently, absorption is too fast (short Tmax, high Cmax). Missing or under-specifying gastric emptying delay, intestinal transit, dissolution/solubility limits, or permeability gradients can all shift the peak earlier and higher.
- t½ is too long (≈ 1164 min vs ≈ 214 min literature) for the same reason as IV: terminal slope underestimation.
- F is high for a high-extraction drug. Overestimation typically reflects Fg/Fh too large—i.e., hepatic or gut intrinsic clearance (CLint) too low or unbound blood fraction (fuB) too high in the well-stirred framework.
### Intepretation
- On central exposure (AUC, Cmax) and F, predictions are within conventional acceptability (mostly ≤2-fold of literature).
- Shape mismatches remain: Tmax too early and tail too long, indicating under-modeled absorption delays and an over-permissive terminal phase.
### Note
The in-vivo values were digitised from published figures (raw datasets were unavailable). Digitisation can introduce small systematic and random errors, so the “Digitised In-Vivo” numbers may not perfectly reflect the original raw values. We therefore compare to both the digitised points and the literature targets.

# Key Takeaways
## Validated IV models
- Rat IV and Human IV reproduced exposure reasonably (AAFE ≈ 1.49 and 1.28; 100% within 2-fold in both datasets).
- CL and AUC∞ were within ~5–20% of literature targets.
## Cross-species translation achieved
- Drug-specific constants (MW, pKa, logP, fup, RB) transferred from rat to human with physiology updated, preserving early/mid-profile accuracy.
## Oral model captures exposure but not shape
- Human PO predicts AUC and Cmax within ~1.1–1.6x of literature but shows earlier Tmax and longer terminal tail (AAFE ≈ 1.79), indicating missing/oversimplified absorption delays and an over-permissive terminal phase.


# Future Work
- gastric emptying and transit to be added on PO absorption equations
- These models can be used with variations in parameters to model disease state (e.g. hepatic impairment).

# References

Jamei, M. et al. "Population-based mechanistic prediction of oral drug absorption." The AAPS Journal, vol. 11, no. 2, 2009, pp. 225–237. doi:10.1208/s12248-009-9099-y.

Jones, H. M., and K. Rowland Yeo. "Basic concepts in physiologically based pharmacokinetic modeling in drug discovery and development." CPT: Pharmacometrics & Systems Pharmacology, vol. 2, no. 8, 2013, pp. 1–12. doi:10.1038/psp.2013.41.

Reigner, B., et al. "Comparative pharmacokinetics of propranolol after administration into the portal and systemic circulation in the rat." Journal of Pharmacology, vol. 38, no. 2, 1989, pp. 112–119. doi:10.1159/000136352.

Rowland, M., et al. "Physiologically based pharmacokinetics in drug development and regulatory science: a workshop report." Clinical Pharmacokinetics, vol. 45, no. 5, 2006, pp. 507–526. doi:10.2165/00003088-200645050-00006.

Rowland, M., and T. N. Tozer. Clinical Pharmacokinetics and Pharmacodynamics: Concepts and Applications. 4th ed., Wolters Kluwer Health/Lippincott Williams & Wilkins, 2011.

Rostami-Hodjegan, A. "Physiologically based pharmacokinetics joined with in vitro–in vivo extrapolation of ADME: a marriage under the arch of systems pharmacology." Clinical Pharmacology & Therapeutics, vol. 92, no. 1, 2012, pp. 50–61. doi:10.1038/clpt.2012.65.

Taegtmeyer, Anne B, et al. A Study of the Relationship between Serum Bile Acids and Propranolol Pharmacokinetics and Pharmacodynamics in Patients with Liver Cirrhosis and in Healthy Controls. Vol. 9, no. 6, 6 June 2014, pp. e97885–e97885, https://doi.org/10.1371/journal.pone.0097885.

Zhao, Peng, et al. "Applications of physiologically based pharmacokinetic (PBPK) modeling and simulation during regulatory review." Clinical Pharmacology & Therapeutics, vol. 92, no. 1, 2012, pp. 1–4. doi:10.1038/clpt.2012.113.
