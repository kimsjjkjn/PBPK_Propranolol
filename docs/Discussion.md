# Discussion
## Rat IV Model
The rat IV model performed well. AAFE was 1.51 for the Time–Concentration profile and 1.16 for pharmacokinetic (PK) parameters. Major PK parameters (t½, CL, Vss, AUC) were all within 2-fold of literature values. For PK parameter comparisons, only the predicted and literature values were compared, because digitised estimates can deviate from the original in vivo data (digitised data were used only for profile-level metrics as raw time-concentration datasets were unavailable). Generally, an AAFE within 2-fold is considered good validation for building robust PBPK models (Deepika and Kumar, 2023). Therefore, these results indicate a robust and credible rat IV model.


## Human IV Model
The human IV model showed AAFE 1.28 for the time–concentration profile and 1.28 for PK parameters, with major PK parameters (t½, CL, Vss, AUC) within 2-fold of literature values. PK parameter comparisons use literature-reported values rather than digitised estimates for the same reason as above.

Although Cmax and Tmax were reported in the literature, these two parameters were not included in the comparison. This is because in the cited study, sampling began after the infusion ended. The first available sample (5 min) is the observed maximum, and with no sample at t = 0, Tmax defaults to 5 min by design. Directly contrasting these with simulations that report concentrations from t = 0 would be misaligned and physiologically uninformative. Accordingly, Cmax and Tmax were excluded from parameter analyses.

Overall, the human IV model demonstrates consistent predictive performance within commonly used 2-fold criteria.

## Human PO Model
The human PO model yielded AAFE 1.76 (time–concentration profile) and 1.43 (PK parameters). Major PK parameters (t½, Tmax, Cmax, AUC, F) were all within 2-fold of literature values. As above, parameter comparisons were made against literature rather than digitised estimates. These findings support that the human PO model also provides acceptable predictive accuracy.


# Model Performance Summary

Table 10. PBPK Propranolol – Model Performance Summary

| Model        |        AAFE (time–concentration) (vs. digitised in vivo) |                          AAFE (PK Parameters) (vs. literature in vivo) | Key Matches (within 2×)       | Key Mismatches                                                           | Overall Conclusion                                                                                           |
| ------------ | -----------------------: | --------------------------------------------: | ----------------------------- | ------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------ |
| **Rat IV**   |                      1.51 |                1.16 | All within 2× | -                                            | Good agreement. Reliable and predictive model.                                 |
| **Human IV** | 1.28 | 1.28 | All within 2×             | - | Good agreement. Reliable and predictive model.           |
| **Human PO** |                     1.76 |         1.43 | All within 2×        | -    |Good agreement. Reliable and predictive model.   |

- Abbreviations: AUC, area under the time-concentration curve; Cmax, peak concentration; CL, clearance; F, oral bioavailability; t½, elimination half-life; Vss, volume of distribution at steady state; Tmax, time point of Cmax.


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

