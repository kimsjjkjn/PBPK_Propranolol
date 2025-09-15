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
| **Rat IV**   |                      1.51 |                1.67 (digitised), 1.36 (literature) | t½, CL, Vss, AUC all within 2× | Slightly high Vss → longer t½                                             | Excellent fit. Exposure (AUC, CL) on target. Reliable and well-validated.                                    |
| **Human IV** | 1.28 | 1.78 (digitised), **2.65 (literature)** | AUC, CL within 2×             | Cmax overpredicted (3×), Tmax mismatch, Vss & t½ strongly overestimated | Partial agreement. Moderate accuracy by 3× rule, but not sufficiently predictive for clinical use.           |
| **Human PO** |                     1.76 |         1.48 (digitised), **1.88 (literature)** | Cmax, Tmax, AUC, F within 2×        | t½ overestimated (~5×)    | Acceptable fit overall. Exposure (AUC, F) well predicted but t½ largely overestimated potentially due to oversimplified absorption model.   |

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


# Future Work
- Current models are the simplest models which are good to start with. More complex factors could be incorporated to better reflect complex mechanisms occuring in actual body. 
- These models can be used with variations in parameters to model disease state (e.g. hepatic impairment).
