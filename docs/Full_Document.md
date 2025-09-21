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
- All equations in PBPK model were manually derived using the basic rationale discussed in the following research paper: https://doi.org/10.2165/00003088-200645050-00006. 
- Values of parameters (fup, RB, CL_int, fu_MP, Molecular Weight, etc.) were obtained from the literature or SimCYP.
  - MW, pKa, logP, fup, RB were drug-specific properties (constant in rat and human models),
  - whilst physiological parameters such as organ volumes/flows, cardiac output, hematocrit, etc. were species-specific parameters (different in rat and human models).
- Kp (tissue-to-plasma partition coefficient) values were obtained in Excel using standard partition coefficient calculators (Poulin–Theil):


  <img width="578" height="327" alt="Screenshot 2025-09-15 at 1 51 55 PM" src="https://github.com/user-attachments/assets/1d280f9c-fe0e-4fa4-8c0f-007078901cff" />

- For derivation of each equation used in model, refer to '**[docs/Model_Derivation.md](docs/Model_Derivation)**' in 'docs' folder.

## Data & Validation
- After completing simulations in Berkeley Madonna, the raw time-concentration datasets were exported to Excel.
- The in-vivo Time-Concentration values were digitised from published figures (as raw datasets were unavailable). Digitisation can introduce small systematic and random errors, so the “Digitised In-Vivo” numbers may not perfectly reflect the original raw values, as also demonstrated in the **Results** section). 
- Simulated and digitised in vivo datasets were overlaid in the same graph in Excel for direct comparison of Time-Concentration profiles.  
- Model performance based on Time-Concentration profile was evaluated by Average Absolute Fold Error (AAFE) and % within 2-fold / 3-fold error ranges (adopted from the following research paper: [https://doi.org/10.2165/00003088-200645050-00006](https://doi.org/10.3390/pharmaceutics14061157)):

   <img width="631" height="291" alt="Screenshot 2025-09-10 at 10 29 07 PM" src="https://github.com/user-attachments/assets/799af2d3-9e5e-4f78-bbb7-2e261a5cb61f" />

  - Note: Because raw time-concentration datasets were not provided by original literature, digitised In Vivo data were used to plot graph and evaluate overall model performance. 
- Key PK parameters (Cmax, Tmax, AUC, t½) from the simulated models were calculated and compared with in vivo PK parameters. The evaluation of model performance based on the calculated PK parameters was done by (adopted from the following research paper: https://doi.org/10.2165/00003088-200645050-00006) calculating:
  - Fold error (FE) per parameter = max(predicted, observed) / min(predicted, observed) so FE ≥ 1.0 by definition.
  - Average-fold error (AFE/AAFE) across parameters = geometric mean of the per-parameter FEs; the paper also reports the % within 2-fold (and 3-fold).
  - Note: As mentioned above, digitisation can introduce small systematic and random errors, so the “Digitised In-Vivo” numbers may not perfectly reflect the original raw values. Therefore both digitised In Vivo parameter values and In Vivo parameter values directly reported by the literature were used to evaluate overall the model performance based on parameters calculated.

# Results

## Rat IV Model
- in vivo pharmacokinetic data for comparison: doi.org/10.1159/000136352



Figure 1. Rat IV: In Vivo figure from the literature (figure 1 control data was used).


<img width="600" height="800" alt="Screenshot 2025-09-10 at 3 13 19 PM" src="https://github.com/user-attachments/assets/e821a4a7-fc80-422e-940d-2287ed015a3b" />

- doi.org/10.1159/000136352



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


Figure 3. Human IV: In Vivo figure from the literature (figure 2A control data was used)
  <img width="711" height="351" alt="Screenshot 2025-09-10 at 2 06 48 PM" src="https://github.com/user-attachments/assets/83b672f8-65d8-4171-b4b3-eead4938a100" />

- 10.1371/journal.pone.0097885

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

Figure 5. Human PO: In Vivo figure from the literature (figure 2B control data was used)
    <img width="711" height="351" alt="Screenshot 2025-09-10 at 2 06 48 PM" src="https://github.com/user-attachments/assets/83b672f8-65d8-4171-b4b3-eead4938a100" />

- 10.1371/journal.pone.0097885

  
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

  
# Discussion
## Rat IV Model
The rat IV model showed excellent performance, with an AAFE of 1.51 based on the time–concentration profile and an AAFE of 1.67 (digitised) and an AAFE of 1.36 (literature) based on the PK parameters. All major pharmacokinetic parameters (t½, CL, Vss, AUC) were predicted within 2-fold of literature values, although t½ was out of 2-fold of digitised values. Yet, it is more appropriate to benchmark against actual literature data rather than digitised estimates, as digitised values may not fully reflect observed in vivo data (except where digitisation is unavoidable, such as for time–concentration profiles). Generally, an AAFE within 2-fold is considered good validation for building robust PBPK models (Deepika et al., 2023). Therefore, this result indicates that the constructed rat IV model is reliable and well validated.

## Human IV Model
Although the comparison with digitised in vivo data yielded an AAFE of 1.28 based on the time–concentration profile and 1.78 based on PK parameters, comparison with literature values gave a higher AAFE of 2.65. As mentioned above, comparison with literature data is more valid and meaningful than with digitised data as digitised data may not be accurate. Prediction error within 3-fold is widely accepted as informative but less reliable than within 2-fold. It is often regarded as moderate accuracy, sometimes acceptable for screening or early development, but usually insufficient for confident clinical application. Therefore, the AAFE of 2.65 based on PK parameters when compared with literature indicates that the model is not reliably predictive in humans. More specifically, while AUC and CL were reproduced reasonably well (within 2-fold), other key parameters including Cmax, Tmax, Vss, and t½ showed large discrepancies (e.g., Cmax was overpredicted by about 3 fold). In particular, the overestimation of Vss and t½ suggests that human IV pharmacokinetics were not adequately captured. Thus, although the human IV model shows partial agreement, it is not clinically predictive.


## Human PO Model
The human PO model showed an AAFE of 1.76 based on the time–concentration profile and 1.48 based on PK parameters when evaluated against digitised PK parameters. Against published literature values, overall error slightly increases (AAFE = 1.88), though it is still within 2-fold. As with the previous cases, comparison with literature data is more meaningful. An AAFE under 2-fold is generally considered acceptable and indicates a reasonably reliable PBPK model. More specifically, while most parameters (Tmax, Cmax, AUC, and F) were well predicted (within 2-fold), t½ was not well reproduced, being overestimated by about 5-fold. In addition to that, although Tmax was within 2-fold, it's slightly earlier than literature value. Largely mismatched t½ and slightly earlier Tmax may be due to overly simplified absorption model that does not account for factors such as gastric emptying, intestinal transit, or reabsorption/secretion. In conclusion, although the human PO model overall demonstrates acceptable prediction, it is not sufficiently predictive for t½.

# Model Performance Summary

- Table 7. PBPK Propranolol – Model Performance Summary

| Model        |        AAFE (Time–Concentration) (digitised) |                          AAFE (PK Parameters) | Key Matches (within 2×)       | Key Mismatches                                                           | Overall Conclusion                                                                                           |
| ------------ | -----------------------: | --------------------------------------------: | ----------------------------- | ------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------ |
| **Rat IV**   |                      1.49 |                1.61 (digitised), 1.31 (literature) | t½, CL, Vss, AUC all within 2× | Slightly high Vss → longer t½                                             | Excellent fit. Exposure (AUC, CL) on target. Reliable and well-validated.                                    |
| **Human IV** | 1.28 | 1.78 (digitised), **2.65 (literature)** | AUC, CL within 2×             | Cmax overpredicted (3×), Tmax mismatch, Vss & t½ strongly overestimated | Partial agreement. Moderate accuracy by 3× rule, but not sufficiently predictive for clinical use.           |
| **Human PO** |                     1.76 |         1.48 (digitised), **1.88 (literature)** | Cmax, Tmax, AUC, F within 2×        | t½ overestimated (~5×)    | Well-validated, acceptable fit overall. Exposure (AUC, F) well predicted but t½ largely overestimated.   |

- Abbreviations: AUC, area under the concentration–time curve; Cmax, peak concentration; CL, clearance; F, oral bioavailability; t½, elimination half-life; Vss, volume of distribution at steady state; Tmax, time point of Cmax.


# Potential Reasons for Discrepancies and Solutions
## High Vss and Longer t½ (Human IV & PO)
In the human IV and PO models, the terminal half-life (t½) and apparent volume of distribution (Vss) were significantly overestimated. 

Propranolol is a highly lipophilic, basic compound (logP ≈ 3–4, pKa ≈ 9–10). Standard Poulin–Theil Kp equations often overpredict tissue partitioning for such drugs, particularly in adipose, skin, and brain, where binding and lysosomal trapping are exaggerated. This in turn inflates Vss (= ∑Kp·V) and prolongs the terminal slope, thus yields a longer terminal half-life.   

However, it is rational to question why rat IV model fit well while human IV showed discrepancies despite the same drug was modeled. This is due to both species-specific physiology and data resolution. 
- Rats have a much smaller proportion of adipose and skin tissue relative to body weight. Even if Kps are overpredicted, the overall contribution to Vss remains limited (which is not the case in humans).
- Rat IV Time-Concentration profiles ended over a shorter window (2 hours). This makes any overestimation of the terminal phase less evident. On the other hand, human IV studies extend sampling period to 48 hours, so the prolonged terminal slope from Kp inflation becomes clearly visible in t½ and Vss.

In addition to this, human Kp values were obtained by scaling rat Kp values with an fup ratio (fup human/fup rat). This empirical adjustment does not fully capture species differences in tissue composition (lipid, water, and protein content) in reality. Therefore, this factor could contribute to yielding less accurate human Kp values, resulting in inflated Vss and thus longer half-life. 

Solution:
- Recalculate Kp using equations proposed by Rodgers-Rowland (base-specific pH-partition and binding) or Schmitt. Use the method that yields the values of Vss and t½ that are closer to the literature values. 
- Use PBPK platforms such as PK-Sim or Simcyp to recalculate Kp values using species-specific tissue composition data rather than using a simple empirical adjustment.

## Cmax Overprediction (Human IV)
Cmax was overpredicted by ~3–4× the literature value.

The model uses a purely perfusion-limited central compartment. This leads to excessively rapid equilibration and a sharper initial peak than observed. In vivo, propranolol shows arteriovenous concentration gradients and red blood cell binding kinetics, which delay the rise in venous plasma concentrations. Because the observed dataset reflects venous plasma samples, the model’s lack of a shallow mixing phase overpredicts the early concentrations. Additionally, possible variability in plasma protein/RBC partitioning during and immediately after infusion may dampen the peak in clinical data, but this dynamic is not represented in the model.

Solution:
- Introduce a fast shallow distribution/mixing compartment (e.g., central venous reservoir or permeability-limited lung/heart) to better reflect the delay before drug appears in peripheral venous plasma.

## Oversimplified Absorption Model (Human PO) - no discrepancy but for future improvement
In the human PO model, oral absorption was represented by a single first-order rate constant (ka) without gastric emptying, intestinal transit, or a lag time. However, propranolol’s absorption is influenced by gastric emptying, regional pH, intestinal permeability, and first-pass intestinal metabolism. In other words, the absorption model is oversimplified and does not sufficiently reflect complex nature of an actual in vivo absorption mechanism. This simplification primarily affects the early profile (Cmax, Tmax) and bioavailability (F). 

Yet, in PO model results, Cmax, Tmax, AUC, and F are all within 2-fold of the literature, indicating that the simple ka model is adequate for the prediction. However, to sufficiently reflect complex mechanism of in vivo absoprtion in the future, it would be more appropriate to use more compelx absorption model rather than this over-simplified model. 

Improvement:
- Use a more mechanistic refinement which would incorporate stomach and intestinal transit compartments (kGE, kT), dynamic intestinal metabolism, and, ultimately, an ACAT-like GI model which accounts for dissolution, solubility, P-gp efflux, and potential enterohepatic recycling to reflect complex nature of absorption in vivo.

# Applications & Future Work
Although this project was originally designed as a proof-of-understanding exercise, the outcomes highlight broader implications for pharmacokinetic modeling in both academic and industrial contexts. 

The rat IV and human PO model achieved close agreement with in vivo data, demonstrating that a first-principles approach can yield robust predictions when physiological parameters are well-defined. By contrast, the discrepancies observed in the human IV simulation underscores the challenges of current simplified models. Although these simplest models are good to start with as modeling beginners, more complex factors could be incorporated to better reflect complex mechanisms occuring in actual body (e.g. by integrating enzyme/transporter contributions and refined absorption modules). 

From a translational perspective, this project also illustrates how a learning-oriented PBPK framework can be developed into more practical applications. 

While the current model was intentionally limited in scope, future extensions could support early drug development (for example, by predicting appropriate dosing regimens or informing preclinical-to-clinical scaling strategies), ultimately helping to minimise wasted resources in identifying the optimal dose.

Similarly, the framework could be adapted to simulate other drug compounds or different patient populations such as pediatrics or geriatrics or patients with hepatic impairment, where physiological parameters diverge markedly from healthy adults. In addition, PBPK modeling can be applied to the development of precision medicine, as physiological parameters can be readily modified within the model to predict unique pharmacokinetic behavior in special populations.

These potential directions highlight how even a learning-oriented model can provide a foundation for models with clinical and regulatory impact.



# Reflection
This independent project on physiologically based pharmacokinetic (PBPK) modeling of propranolol was conducted using Berkeley Madonna, with all organ-level differential equations derived from first principles. By constructing and validating rat (IV) and human (IV and PO) models, I developed hands-on experience in mechanistic model building, parameterization, and quantitative evaluation of model performance.

The project successfully validated the rat IV and human PO models, while also identifying key limitations in the human IV model and outlining directions for refinement. As a first attempt at PBPK modeling, the models were quite simplified. Therefore, future improvements including incorporating gastric emptying and intestinal transit into the oral absorption module and integrating transporter and enzyme dynamics should be done to reflect more complex in vivo mechanism.

Beyond the technical implementation, this project strengthened my understanding of PBPK mechanisms, provided practice in complete ODE derivation, and reinforced systematic model validation using fold-error metrics (FE, AAFE, within 2×/3×). Importantly, it highlighted both the strengths and challenges of PBPK modeling: exposure-based parameters can be reproduced with reasonable accuracy, but shape-dependent outcomes such as Tmax and terminal half-life require greater physiological complexity.

Overall, this work served as both a validated case study and a foundation for future extensions toward clinically predictive PBPK modeling.



# References

Brown, Ronald P., et al. “Physiological Parameter Values for Physiologically Based Pharmacokinetic Models.” Toxicology and Industrial Health, vol. 13, no. 4, July 1997, pp. 407–484. https://doi.org/10.1177/074823379701300401.

Deepika, Deepika, and Vikas Kumar. “The Role of ‘Physiologically Based Pharmacokinetic Model (PBPK)’ New Approach Methodology (NAM) in Pharmaceuticals and Environmental Chemical Risk Assessment.” International Journal of Environmental Research and Public Health, vol. 20, no. 4, 16 Feb. 2023, p. 3473. https://doi.org/10.3390/ijerph20043473.

DrugBank. “Propranolol.” Go.drugbank.com, 13 June 2024. https://go.drugbank.com/drugs/DB00571.

Evans, Gwyn H., et al. “The Disposition of Propranolol. III. Decreased Half-Life and Volume of Distribution as a Result of Plasma Binding in Man, Monkey, Dog and Rat.” The Journal of Pharmacology and Experimental Therapeutics, vol. 186, no. 1, 31 Jan. 2025, pp. 114–122. https://doi.org/10.1016/S0022-3565(25)29572-6.

Hung, Daniel Y., et al. “Disposition Kinetics of Propranolol Isomers in the Perfused Rat Liver.” The Journal of Pharmacology and Experimental Therapeutics, vol. 311, no. 2, 3 Jan. 2025, pp. 822–829. https://doi.org/10.1124/jpet.104.070011.

Jamei, M., et al. “Population-Based Mechanistic Prediction of Oral Drug Absorption.” The AAPS Journal, vol. 11, no. 2, 2009, pp. 225–237. https://doi.org/10.1208/s12248-009-9099-y.

Jones, H. M., and K. Rowland Yeo. “Basic Concepts in Physiologically Based Pharmacokinetic Modeling in Drug Discovery and Development.” CPT: Pharmacometrics & Systems Pharmacology, vol. 2, no. 8, 2013, pp. 1–12. https://doi.org/10.1038/psp.2013.41.

Jones, Hannah M., et al. “A Novel Strategy for Physiologically Based Predictions of Human Pharmacokinetics.” Clinical Pharmacokinetics, vol. 45, no. 5, 2006, pp. 511–542. https://doi.org/10.2165/00003088-200645050-00006.

Kaufman, Daniel P., et al. “Physiology, Glomerular Filtration Rate (GFR).” StatPearls Publishing, National Library of Medicine, 2023. https://www.ncbi.nlm.nih.gov/books/NBK500032/.

Lee, H. B., and M. D. Blaufox. “Blood Volume in the Rat.” Journal of Nuclear Medicine, vol. 26, no. 1, Jan. 1985, pp. 72–6. https://pubmed.ncbi.nlm.nih.gov/3965655/.

Lee, Myongjae, et al. “Prediction of Pharmacokinetics of IDP-73152 in Humans Using Physiologically-Based Pharmacokinetics.” Pharmaceutics, vol. 14, no. 6, 28 May 2022, p. 1157. https://doi.org/10.3390/pharmaceutics14061157.

Mondal, Himel, and Saran Lotfollahzadeh. “Hematocrit (HCT).” StatPearls Publishing, Nih.gov, 6 Oct. 2024. https://www.ncbi.nlm.nih.gov/books/NBK542276/.

Nicolaï, J., et al. “Verapamil Hepatic Clearance in Four Preclinical Rat Models: Towards Activity‐Based Scaling.” Biopharmaceutics & Drug Disposition, vol. 36, no. 7, 11 May 2015, pp. 462–480. https://doi.org/10.1002/bdd.1959.

Potter, D., et al. “Character of Function and Size in Kidney during Normal Growth of Rats.” Pediatric Research, vol. 3, no. 1, 1 Jan. 1969, pp. 51–59. https://doi.org/10.1203/00006450-196901000-00007.

Reigner, B., et al. “Comparative Pharmacokinetics of Propranolol after Administration into the Portal and Systemic Circulation in the Rat.” Journal of Pharmacology, vol. 38, no. 2, 1989, pp. 112–119. https://doi.org/10.1159/000136352.

Rostami-Hodjegan, A. “Physiologically Based Pharmacokinetics Joined with In Vitro–In Vivo Extrapolation of ADME: A Marriage under the Arch of Systems Pharmacology.” Clinical Pharmacology & Therapeutics, vol. 92, no. 1, 2012, pp. 50–61. https://doi.org/10.1038/clpt.2012.65.

Rowland, M., et al. “Physiologically Based Pharmacokinetics in Drug Development and Regulatory Science: A Workshop Report.” Clinical Pharmacokinetics, vol. 45, no. 5, 2006, pp. 507–526. https://doi.org/10.2165/00003088-200645050-00006.

Rowland, M., and T. N. Tozer. Clinical Pharmacokinetics and Pharmacodynamics: Concepts and Applications. 4th ed., Wolters Kluwer Health/Lippincott Williams & Wilkins, 2011.

Shand, D. G., et al. “The Disposition of Propranolol.” Pharmacology, vol. 8, no. 4–6, 1 Jan. 1972, pp. 344–352. https://doi.org/10.1159/000136352.

Silberx, Bernie M., et al. “Dose-Dependent Elimination of Propranolol and Its Major Metabolites in Humans.” Journal of Pharmaceutical Sciences, vol. 72, no. 7, 1 July 1983, pp. 725–732. https://doi.org/10.1002/jps.2600720703.

Simcyp Simulator. Version 22, Certara UK Limited, 2023.

Singh, K., et al. “Determination of in Vivo Hepatic Extraction Ratio from in Vitro Metabolism by Rat Hepatocytes.” Drug Metabolism and Disposition, vol. 19, no. 5, 1991, pp. 990–6. https://pubmed.ncbi.nlm.nih.gov/1686248/.

Taegtmeyer, Anne B., et al. “A Study of the Relationship between Serum Bile Acids and Propranolol Pharmacokinetics and Pharmacodynamics in Patients with Liver Cirrhosis and in Healthy Controls.” PLoS ONE, vol. 9, no. 6, 6 June 2014, pp. e97885–e97885. https://doi.org/10.1371/journal.pone.0097885.

Taylor, E. A., and P. Turner. “The Distribution of Propranolol, Pindolol and Atenolol between Human Erythrocytes and Plasma.” British Journal of Clinical Pharmacology, vol. 12, no. 4, Oct. 1981, pp. 543–548. https://doi.org/10.1111/j.1365-2125.1981.tb01263.x.

Zhao, Peng, et al. “Applications of Physiologically Based Pharmacokinetic (PBPK) Modeling and Simulation during Regulatory Review.” Clinical Pharmacology & Therapeutics, vol. 92, no. 1, 2012, pp. 1–4. https://doi.org/10.1038/clpt.2012.113.
