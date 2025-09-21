# Model Derivation
- All equations in PBPK model were manually derived using the basic rationale discussed in the following research paper: https://doi.org/10.2165/00003088-200645050-00006.
  - All images/figures of certain equations in this page are from this research paper. 
- A physiologically based, perfusion-limited, well-stirred PBPK model was implemented for rat IV, human IV, and human PO simulations.
- All models are in the standard of blood concentration. Therefore, `fub (= fup / RB)` (unbound drug fraction in blood) is used to maintain the standard if needed.
  - Models may be built on plasma concentration, but the standard (blood vs. plasma) must remain consistent across the model.
- **Note: a semicolon (;) in codes indicates a comment and is not executed as part of the code.**
    
# Parameters To Prepare
- Parameter values that are directly brought from literature or SimCYP include:
  - **Drug-specific parameters**:
    - fup (unbound drug fraction in plasma)
    - RB (ratio blood:plasma)
    - MW (Molecular Weight)
  - **Species-specific parameters**:
    - GFR (Glomerular Filtration Rate)
    - Hematocrit (Hct)
    - Tissue volume (V)
    - Blood flow (Q)
    - Weight (body weight & organ weight)
    - Hepatic IVIVE scaling factor: MPPGL (microsomal protein per gram liver (mg/g liver))
  - **Species and drug-specific parameters**:
    - CL_int (intrinsic clearance)
    - fu_MP (unbound drug fraction in microsomal incubation)
    - Fobs (known/reported bioavailability)

## Parameter–Reference Tables

Table 1. Parameters obtained from literature that are used to construct **rat IV model** and their references

| Parameter | Unit | Value (Baseline) | Source / Reference | Notes (Assumptions, Comments) |
|-----------|------|------------------|--------------------|-------------------------------|
| fup | - | 0.08 | EVANS, GWYN H., et al. “THE DISPOSITION of PROPRANOLOL. III. DECREASED HALF-LIFE and VOLUME of DISTRIBUTION as a RESULT of PLASMA BINDING in MAN, MONKEY, DOG and RAT.” The Journal of Pharmacology and Experimental Therapeutics, vol. 186, no. 1, 31 Jan. 2025, pp. 114–122, https://doi.org/10.1016/S0022-3565(25)29572-6. | The binding of propranolol to plasma has been determined at therapeutic concentrations by equilibrium dialysis in rat (92.2%), thus fup is (100-92.2)/100 = 0.078 ≈ 0.08 |
| RB | - | 0.78 | "Singh, K, et al. “Determination of in vivo Hepatic Extraction Ratio from in Vitro Metabolism by Rat Hepatocytes.” Drug Metabolism and Disposition: The Biological Fate of Chemicals, vol. 19, no. 5, 1991, pp. 990–6, pubmed.ncbi.nlm.nih.gov/1686248/. | - |
| GFR_rat | mL/min | 2.9 | "Potter, D, et al. “Character of Function and Size in Kidney during Normal Growth of Rats.” Pediatric Research, vol. 3, no. 1, 1 Jan. 1969, pp. 51–59, https://doi.org/10.1203/00006450-196901000-00007. | The mean GFR is reported as 1.7 mL/min for rats with an average body weight of 173 g and 4.1 mL/min for rats with an average body weight of 350 g. Since the present IV model is standardised to a rat body weight of 250 g, the average of these two values (2.9 mL/min) was adopted. This approximation is justified because the interpolated body weight (260 g) closely matches the model reference of 250 g. |
| CL_int | mL/min/mg microsomal protein | 0.13 | "Hung, Daniel Y., et al. “Disposition Kinetics of Propranolol Isomers in the Perfused Rat Liver.” The Journal of Pharmacology and Experimental Therapeutics, vol. 311, no. 2, 3 Jan. 2025, pp. 822–829, www.sciencedirect.com/science/article/pii/S0022356524316593, https://doi.org/10.1124/jpet.104.070011. | - |
| fu_MP | - | 0.49 | "Hung, Daniel Y., et al. “Disposition Kinetics of Propranolol Isomers in the Perfused Rat Liver.” The Journal of Pharmacology and Experimental Therapeutics, vol. 311, no. 2, 3 Jan. 2025, pp. 822–829, www.sciencedirect.com/science/article/pii/S0022356524316593, https://doi.org/10.1124/jpet.104.070011. | - |
| MW | g/mol | 259.3434 | DrugBank. “Propranolol.” Go.drugbank.com, 13 June 2024, go.drugbank.com/drugs/DB00571. | - |
| Hct | - | 0.45 | "Lee, H B, and M D Blaufox. “Blood Volume in the Rat.” Journal of Nuclear Medicine : Official Publication, Society of Nuclear Medicine, vol. 26, no. 1, Jan. 1985, pp. 72–6, pubmed.ncbi.nlm.nih.gov/3965655/. | 0.45 (45%) was set as the representative hematocrit, as Lee & Blaufox (1985) reported hematocrit values of 43.94 ± 2.77% for rats with body weight >120 g, and 42.30 ± 3.39% for male rats. |
| Tissue volume | mL | Check 'Rat IV code' under 'code' folder | "Brown, Ronald P., et al. “Physiological Parameter Values for Physiologically Based Pharmacokinetic Models.” Toxicology and Industrial Health, vol. 13, no. 4, July 1997, pp. 407–484, https://doi.org/10.1177/074823379701300401. | - |
| Blood flow | mL/min | Check 'Rat IV code' under 'code' folder | Simcyp Simulator. Version 22, Certara UK Limited, 2023. | - |
| Weight | g | Check 'Rat IV code' under 'code' folder | "Brown, Ronald P., et al. “Physiological Parameter Values for Physiologically Based Pharmacokinetic Models.” Toxicology and Industrial Health, vol. 13, no. 4, July 1997, pp. 407–484, https://doi.org/10.1177/074823379701300401. | Obtained by multiplying the relative organ weights (% of body weight) reported in Brown et al. (1997) by a 250 g rat body weight. |
| MPPGL_mic | mg microsomal protein / g liver | 44.5 | "J. Nicolaï, et al. “Verapamil Hepatic Clearance in Four Preclinical Rat Models: Towards Activity‐Based Scaling.” Biopharmaceutics & Drug Disposition, vol. 36, no. 7, 11 May 2015, pp. 462–480, https://doi.org/10.1002/bdd.1959. | - |

Table 2. Parameters obtained from literature that are used to construct **human IV model** and their references

| Parameter | Symbol/Unit | Value (Baseline) | Source / Reference | Notes (Assumptions, Comments) |
|-----------|-------------|------------------|--------------------|-------------------------------|
| fup | - | 0.1138 | Taylor, EA, and P Turner. “The Distribution of Propranolol, Pindolol and Atenolol between Human Erythrocytes and Plasma.” British Journal of Clinical Pharmacology, vol. 12, no. 4, Oct. 1981, pp. 543–548, https://doi.org/10.1111/j.1365-2125.1981.tb01263.x. | Propranolol is reported to be 88.62 + 0.93% protein bound in plasma. Thus, fup is (100-88.62)/100=0.1138. |
| RB | - | 0.74 | Taylor, EA, and P Turner. “The Distribution of Propranolol, Pindolol and Atenolol between Human Erythrocytes and Plasma.” British Journal of Clinical Pharmacology, vol. 12, no. 4, Oct. 1981, pp. 543–548, https://doi.org/10.1111/j.1365-2125.1981.tb01263.x. | - |
| GFR_human | mL/min | 120 | "Kaufman, Daniel P, et al. “Physiology, Glomerular Filtration Rate (GFR).” National Library of Medicine, StatPearls Publishing, 2023, www.ncbi.nlm.nih.gov/books/NBK500032/. | - |
| CL_int_eff | mL/min | 2710 | Silberx, Bernie M, et al. “Dose-Dependent Elimination of Propranolol and Its Major Metabolites in Humans.” Journal of Pharmaceutical Sciences, vol. 72, no. 7, 1 July 1983, pp. 725–732, https://doi.org/10.1002/jps.2600720703. | "Kornhauser et al. (31) reported an average intrinsic clearance (CLint) of 2.71 liter/min on whole blood concentrations)". Thus, this intrinsic clearance value is already in vivo scaled and in the standard of blood concentration. |
| MW | g/mol | 259.3434 | DrugBank. “Propranolol.” Go.drugbank.com, 13 June 2024, go.drugbank.com/drugs/DB00571. | - |
| Hct | - | 0.45 | "Mondal, Himel, and Saran Lotfollahzadeh. “Hematocrit (HCT).” Nih.gov, StatPearls Publishing, 6 Oct. 2024, www.ncbi.nlm.nih.gov/books/NBK542276/. | Hematocrit was set to 0.45 (45%), representing the mid-point of normal adult ranges (men 40–54%, women 36–48%). |
| Tissue volume | mL | Check 'Human IV code' under 'code' folder | Simcyp Simulator. Version 22, Certara UK Limited, 2023. | - |
| Blood flow | mL/min | Check 'Human IV code' under 'code' folder | Simcyp Simulator. Version 22, Certara UK Limited, 2023. | - |


Table 3. Parameters obtained from literature that are used to construct **human PO model** and their references

| Parameter | Symbol/Unit | Value (Baseline) | Source / Reference | Notes (Assumptions, Comments) |
|-----------|-------------|------------------|--------------------|-------------------------------|
| fup | - | 0.1138 | Taylor, EA, and P Turner. “The Distribution of Propranolol, Pindolol and Atenolol between Human Erythrocytes and Plasma.” British Journal of Clinical Pharmacology, vol. 12, no. 4, Oct. 1981, pp. 543–548, https://doi.org/10.1111/j.1365-2125.1981.tb01263.x. | Propranolol is reported to be 88.62 + 0.93% protein bound in plasma. Thus, fup is (100-88.62)/100=0.1138. |
| RB | - | 0.74 | Taylor, EA, and P Turner. “The Distribution of Propranolol, Pindolol and Atenolol between Human Erythrocytes and Plasma.” British Journal of Clinical Pharmacology, vol. 12, no. 4, Oct. 1981, pp. 543–548, https://doi.org/10.1111/j.1365-2125.1981.tb01263.x. | - |
| GFR_human | mL/min | 120 | "Kaufman, Daniel P, et al. “Physiology, Glomerular Filtration Rate (GFR).” National Library of Medicine, StatPearls Publishing, 2023, www.ncbi.nlm.nih.gov/books/NBK500032/. | - |
| CL_int_eff | mL/min | 2710 | Silberx, Bernie M, et al. “Dose-Dependent Elimination of Propranolol and Its Major Metabolites in Humans.” Journal of Pharmaceutical Sciences, vol. 72, no. 7, 1 July 1983, pp. 725–732, https://doi.org/10.1002/jps.2600720703. | "Kornhauser et al. (31) reported an average intrinsic clearance (CLint) of 2.71 liter/min on whole blood concentrations)". Thus, this intrinsic clearance value is already in vivo scaled and in the standard of blood concentration. |
| Fobs | - | 0.27 | "Taegtmeyer, Anne B, et al. A Study of the Relationship between Serum Bile Acids and Propranolol Pharmacokinetics and Pharmacodynamics in Patients with Liver Cirrhosis and in Healthy Controls. Vol. 9, no. 6, 6 June 2014, pp. e97885–e97885, https://doi.org/10.1371/journal.pone.0097885. | - |
| MW | g/mol | 259.3434 | DrugBank. “Propranolol.” Go.drugbank.com, 13 June 2024, go.drugbank.com/drugs/DB00571. | - |
| Hct | - | 0.45 | "Mondal, Himel, and Saran Lotfollahzadeh. “Hematocrit (HCT).” Nih.gov, StatPearls Publishing, 6 Oct. 2024, www.ncbi.nlm.nih.gov/books/NBK542276/. | Hematocrit was set to 0.45 (45%), representing the mid-point of normal adult ranges (men 40–54%, women 36–48%). |
| Tissue volume | mL | Check 'Human IV code' under 'code' folder | Simcyp Simulator. Version 22, Certara UK Limited, 2023. | - |
| Blood flow | mL/min | Check 'Human IV code' under 'code' folder | Simcyp Simulator. Version 22, Certara UK Limited, 2023. | - |


# Abbreviation
- Tissue (T)
- Volume (V)
- Blood flow (Q)
- Hematocrit (Hct)
- Weight (W)
- Vein (ve)
- Artery (ar)
- Adipose (a)
- Bone (bo)
- Brain (b)
- Gut (g)
- Heart (h)
- Kidneys (k)
- Liver (li)
- Lung (lg)
- Muscle (m)
- Plasma (p)
- Skin (sk)
- Spleen (sp)

# Rat IV Model

## Period setting
*Note: The period setting should be aligned with the literature conditions to ensure valid comparison.*

### **CODE**:
- `STARTTIME = 0` ; Simulation start time (min)
- `STOPTIME = 120` ; Simulation end time (min)
- `DT = 0.001`; Solver integration step (min). Smaller → more accurate (slower); larger → faster but risk of error.
- `DTOUT = 1`; Output sampling interval (min). Results are recorded/shown every 1 min (doesn’t affect dynamics).

## Administration
*Note: The administration setting should be aligned with the literature conditions to ensure valid comparison.*

### **CODE**:
- `dose_IV = 2500000 * BW/1000  ;ng ;(BW/1000=kg)`
  - Defines the total IV dose in nanograms (ng).
  - Because 2500000 is in the unit of ng/kg, body weight in kilograms (kg) must be multiplied to change the unit to ng. 
    - `BW/1000` converts body weight from grams (g) to kilograms (kg), since dosing is usually expressed per kg.
- `dosing_time_IV = 30/60 ;min`
  - Defines the infusion duration in minutes.
  - `30/60 = 0.5 min` means the infusion lasts 30 seconds
- `IV_input = IF t< dosing_time_IV THEN dose_IV/dosing_time_IV ELSE 0`
  - Defines the infusion rate (ng/min) as a time-dependent input.
  - If the simulation time `t` is still within the infusion window (`t < dosing_time_IV`), drug is delivered at a constant rate (`Rate = Total dose / Infusion duration`)
  - Once infusion time is over (`t ≥ dosing_time_IV`), the input is set to 0, meaning no more drug enters the system.

## EP Calculation

### **CODE**:
- `EP = 1 + (RB-1)/Hct`

### **Derivation**:

Definition:
- `C_blood` : drug concentration in whole blood
- `C_plasma` : drug concentration in plasma
- `C_RBC` : drug concentration inside red blood cells (RBCs)
- `EP`: Erythrocyte-to-plasma concentration ratio (RBC concentration / plasma concentration), unitless
- `RB` : Blood-to-plasma concentration ratio (C_blood / C_plasma), unitless.
- `Hct` : Hematocrit (fraction of blood volume occupied by RBCs, 0–1), unitless.

**`EP` Derivation**:
- Blood is a mixture of RBCs (`Hct` fraction) and plasma (`1−Hct` fraction).
  - Therefore, Whole blood = RBCs (`Hct` of volume) + plasma (`1 − Hct` of volume).
  - Thus the blood concentration is the volume-weighted average of the two phases:
    - `C_blood = Hct * C_RBC + (1 − Hct) * C_plasma`
  - Normalize to plasma (divide both sides by `C_plasma`)
    - `C_blood / C_plasma = Hct * (C_RBC / C_plasma) + (1 − Hct)`
  - Identify ratios:
    - `RB = C_blood / C_plasma`
    - `EP = C_RBC / C_plasma`
  - Result:
    - `RB = Hct * EP + (1 − Hct)`
- Solve for `EP`:
    1. Start from the mixture identity:
      - `RB = Hct * EP + (1 − Hct)`
    2. Move the plasma term to the left:
      - `RB − (1 − Hct) = Hct * EP`
    3. Divide by Hct:
      - `EP = (RB − (1 − Hct)) / Hct`
      - Compact forms (equivalent): `EP = 1 + (RB − 1)/Hct`


## Vss Calculation

### **CODE**:
- `Vss = EP * (Vve+Var) * Hct + (Vve+Var) * (1-Hct) + Kp_a * Va + Kp_bo * Vbo + Kp_b * Vb + Kp_g * Vg + Kp_h * Vh + Kp_k * Vk + Kp_li * Vli + Kp_lg * Vlg + Kp_m * Vm + Kp_sk * Vsk + Kp_sp * Vsp ; plasma Vss`
- `Vss_b = Vss / RB`

### **Derivation**:

Definition:
- `(Vve + Var)`: Total blood volume represented as venous + arterial compartments.
- Hct: Hematocrit (fraction of blood volume that is red blood cells).
- EP: Erythrocyte-to-plasma concentration ratio (RBC concentration / plasma concentration), dimensionless.

Blood contribution (plasma-referenced):
  - `EP * (Vve+Var) * Hct`: Drug contained inside RBCs, expressed relative to plasma concentration.
  - `(Vve+Var) * (1−Hct)`: Drug contained in plasma itself.
  - Together these two terms = blood volume × blood:plasma partition `(Hct⋅EP+(1−Hct))`.

Tissue contributions (plasma-referenced):
- `Kp_T * VT` terms (for a, bo, b, g, h, k, li, lg, m, sk, sp):
  - `Kp_T` = tissue-to-plasma partition coefficient of tissue i (dimensionless).
  - `VT`= anatomical volume of tissue i (e.g., `Va` adipose, `Vbo` bone, `Vb` brain, `Vg` gut, `Vh` heart, `Vk` kidney, `Vli` liver, `Vlg` lung, `Vm` muscle, `Vsk` skin, `Vsp` spleen).
  - Each product `Kp_T * VT` adds that tissue’s effective distribution volume referenced to plasma.

What the equation is doing:
- It sums blood (RBC + plasma) distribution and all tissue distributions, all referenced to plasma concentration, to yield the steady-state volume of distribution vs. plasma (`Vss, plasma`).

Units:
- All volumes V in mL and EP, Hct, Kp are unitless → `Vss` returns in mL.

**`Vss_b`**
- `Vss`, as explained above, is plasma-referenced. Therefore, if literature concentrations are reported in plasma, this Vss value should be used.
- Yet, if literature concentrations are reported in blood, `Vss` cannot be used but should be converted to blood-level (= `Vss_b`. This can be done by dividing `Vss` by `RB`.
  - **`Vss_b` Derivation**:
    - `Vss,plasma ​= Amount in body​ / C_plasma​`
      - Where `Vss,plasma` = plasma-referenced Vss
      - `C_plasma` = Drug concentration in plasma
    - `Vss,blood ​= Amount in body​ / C_blood​`
      - Where `Vss,blood` = blood-referenced Vss
      - `C_blood` = Drug concentration in blood
    - `C_blood = C_plasma * RB`
    - Thus, `Vss,blood` = `Amount in body​ / C_blood` = `Amount in body​ / (C_plasma * RB)` = `(Amount in body​/C_plasma) * (1/RB)` = `Vss,plasma / RB`.


## Predicted Kp values
Kp (tissue-to-plasma partition coefficient) values were obtained using standard partition coefficient calculators (Poulin–Theil): 

  <img width="578" height="327" alt="Screenshot 2025-09-15 at 1 51 55 PM" src="https://github.com/user-attachments/assets/1d280f9c-fe0e-4fa4-8c0f-007078901cff" />

## Metabolism & Excretion
### Renal Clearance
#### **CODE**:
- `GFR_rat = 2.9 ;mL/min`
- `CL_r = (fup/RB * GFR_rat) ;mL/min ; fub = fup/RB`
- `CL_r_u = GFR_rat`
#### **Derivation**:
- Definitions
  - `CL_r_blood = elimination_rate / C_blood`
  - `CL_r_u = elimination_rate / C_unbound`
  - `C_unbound = fub * C_blood`
  - `fub = fup / RB`

- Filtration removes only UNBOUND drug:
  - `elimination_rate` = `C_unbound * GFR` = `(fub * C_blood) * GFR`

- Therefore (algebra):
  - `CL_r_blood` = `(fub * C_blood * GFR) / C_blood` = `fub * GFR`
  - `CL_r_u` = `(fub * C_blood * GFR) / (fub * C_blood)` = `GFR`

### **Renal Excretion**: 
#### **CODE**:
- `Xexc_r = CL_r_u * (C_k * (1/Kp_k)) * fup`
#### **Derivation**:

<img width="327" height="68" alt="Screenshot 2025-09-12 at 9 29 51 PM" src="https://github.com/user-attachments/assets/14f18d62-a625-4829-b64d-e77e34b469d5" />

- In this Mass balance differential equation of kidney tissue, the excretion equation is `CL_R_u * Cv_k_u`.
- `Cv_k_u = Cv_k * fub` ; fub is multiplied to obtain unbound drug concentration in venous 'blood'.
  - `Cv_k = C_k * (1/Kp_k) * RB`
    - *Please refer to **Non-Eliminating Tissue Differential Equation Derivation** in **Rat IV Model - Differential Equation** section for the derivation of `Cv_k`.*
  - `fub = fup / RB`
- Thus `Cv_k_u` = `C_k * (1/Kp_k) * RB * (fup / RB)` = `C_k * (1/Kp_k)) * fup`
- Therefore, `Xexc_r = CL_r_u * (C_k * (1/Kp_k)) * fup`

### **CL_int_u**: 
#### **CODE**:
- `CL_int = 0.13 * MPPGL_mic * W_li ;mL/min`
- `fu_MP = 0.49`
- `CL_int_u = CL_int / fu_MP`


#### **Derivation**:
- `CL_int = 0.13` is microsomal intrinsic clearance obtained from literature and is in the unit of mL/min/mg microsomal protein. `MPPGL_mic * W_li` is multiplied for in vivo scaling.
  - `MPPGL_mic`: mg microsomal protein / g liver.
  - `W_li`: liver weight (g).
  - Unit check: *(mL/min/mg) × (mg/g) × (g) = mL/min* → whole-liver intrinsic clearance.
- `fu_MP = 0.49` is unbound fraction in microsomal incubation.
  - *Note: If CL_int is determined from hepatocyte or S9 incubations, apply the appropriate scaling factors and unbound fraction as follows:*
    - *HPGL – hepatocytes per gram liver (cells/g liver)*
    - *S9PGL – S9 protein per gram liver (mg/g liver)*
- `CL_int_u`, i.e. unbound intrinsic clearance is obtained by dividing `CL_int` (whole-liver intrinsic clearance) value by `fu_MP` (unbound fraction in microsomal incubation).
  - The enzyme only “sees” **unbound** drug. In incubation:
    - `fu_MP` = `C_unbound / C_total`  (fraction unbound in incubation)
  - Metabolic rate follows the free-drug hypothesis: `rate = CL_int_u * C_unbound`
    - Thus `CL_int` = `rate / C_total` = `(CL_int_u * C_unbound) / C_total` = `CL_int_u * (C_unbound / C_total)` = `CL_int_u * fu_MP`
    - Thus, `CL_int_u = CL_int / fu_MP`

### **Hepatic Metabolism**: 
#### **CODE**:
- `Xmet_li = CL_int_u * (C_li * (1/Kp_li)) * fup`   
#### **Derivation**:

<img width="440" height="65" alt="Screenshot 2025-09-12 at 9 28 38 PM" src="https://github.com/user-attachments/assets/d07a1076-3a10-4f21-b06e-1f864a26741d" />

- In this Mass balance differential equation of liver tissue, the metabolism equation is `in vivo CL_int_u * Cv_li_u`.
- `Cv_li_u = Cv_li * fub` ; fub is multiplied to obtain unbound drug concentration in venous 'blood'.
  - `Cv_li = C_li * (1/Kp_li) * RB`
    - *Please refer to **Non-Eliminating Tissue Differential Equation Derivation** in **Rat IV Model - Differential Equation** section for the derivation of `Cv_li`.*
  - `fub = fup / RB`
- Thus `Cv_li_u` = `C_li * (1/Kp_li) * RB * (fup / RB)` = `C_li * (1/Kp_li)) * fup`
- Therefore, `Xmet_li = CL_int_u * (C_li * (1/Kp_li)) * fup`



## **Differential Equations**: 

**Non-Eliminating Tissue Differential Equation Derivation**:

<img width="577" height="180" alt="Screenshot 2025-09-12 at 9 32 08 PM" src="https://github.com/user-attachments/assets/5619ac97-93c3-4bde-9899-952cd3c72a33" />

- `VT * d/dt(C_T) = Q_T * C_ar - Q_T * Cv_T`
  - Mass in: `Q_T * C_ar`
  - Mass out: `Q_T * Cv_T`
  - There is no differential equation for `Cv_T` as blood outflow is different depending on the tissues. Therefore, the following conversion is used to define `Cv_T`:
    - `Kp_T = C_T / C_p` ; `C_T` = tissue concentration, `C_P` = plasma concentration
    - Thus `C_p = C_T / Kp_T`
    - `Cv_T = C_p * RB` ; RB is multiplied to convert the standard from plasma to blood concentration
    - Thus `Cv_T = (C_T / Kp_T) * RB`
  - Thus, non-eliminating tissue differential equation can be written again as:
    `VT * d/dt(C_T) = (Q_T * C_ar) - (Q_T * (C_T / Kp_T) * RB)`

**Mass Differential Equations**
- **Structure**:
  - In the model, Mass in and Mass out are defined separately and each defined terms are used collectively to express mass differential equations.
  - **Basic structure of mass differential equation**: `d/dt(C_T) = (1/VT) * (Xin_T - Xout_T)`
    - This basic structure is directly applied to mass differential equations of artery, adipose, bone, brain, heart, lung, muscle, skin, and spleen.
    - The following tissues had slight variations in mass differential equations:
      - **Vein**: `d/dt(C_ve) = (1/Vve) * (IV_input + Xin_ve - Xout_ve)`
        - `IV_input` (= `IF t< dosing_time_IV THEN dose_IV/dosing_time_IV ELSE 0`) is added in vein mass differential equation to reflect the fact that the during the infusion period, the specific amount of drug is directly introduced to the venous blood.
      - **Gut**: `d/dt(C_g) = (1/Vg) * (Xin_g - Xout_g + Rabs)`
        - Gut is where absorption of drug occurs. Therefore, absorption rate (= `Rabs`) is added to the basic structure in the case of PO model.
        - Because absorption does not occur in the case of IV administration (thus put as `Rabs = 0` in IV model), gut mass differential equation is the same as the basic structure in IV model (but this is not the case for PO model - see Rabs derivation in **Human PO Model - Absorption** section below).
      - **Kidney**: `d/dt(C_k) = (1/Vk) * (Xin_k - Xout_k - Xexc_r)`
        - To reflect renal excretion, `Xexc_r` is incorporated in the equation (because excreted amount = `Xexc_r` is removed from total kidney concentration, `Xexc_r` is subtracted).
      - **Liver**: `d/dt(C_li) = (1/Vli) * (Xin_li - Xout_li - Xmet_li)`
        - To reflect hepatic metabolism, `Xmet_li` is incorporated in the equation (because metabolised amount = `Xmet_li` is removed from total liver concentration, `Xmet_li` is subtracted).
- **Mass in**
  - Basic structure of mass in equation `(Xin_T): Xin_T = Q_T * C_ar`
    - Arterial blood delivers drug to tissues, therefore inflow uses the **arterial blood concentration** `C_ar` (not `C_T`).
    - This basic structure is directly applied to mass in equation of adipose, bone, brain, gut, heart, kidney, muscle, skin, and spleen.
    - The following tissues had slight variations in mass in equations:
      - **Artery**: `Xin_ar = Xout_lg`
        - `Xout_lg` = `Q_lg * Cv_lg` = `Q_lg * C_lg * (1/Kp_lg) * RB`
          - *Please refer to **Non-Eliminating Tissue Differential Equation Derivation** in **Rat IV Model - Differential Equation** section for the derivation of `Cv_lg`.*

        - `Xin_ar` (arterial inflow) is equivalent to `Xout_lg` (pulmonary outflow) because blood leaving the lung (pulmonary vein) is the direct source of systemic arterial blood. Therefore, drug concentration of pulmonary vein is equivalent to the drug concentration of systemic arterial blood. 
      - **Vein**: `Xin_ve = Xout_a + Xout_bo + Xout_b + Xout_h + Xout_k + Xout_li + Xout_m + Xout_sk`
        - Because vein compartment is where blood that outflow from each tissue is assembled, `Xin_ve` (venous inflow) equals the sum of tissue outflows excluding artery, lung, and the portal-drained organs (gut, spleen - which reach the systemic vein via the liver). This is because:
          -  **Artery**: Artery is not a venous source. Arterial outflow distributes to organs and only after tissues do those flows rejoin the vein.
          -  **Lung**: Vein → lung → artery are in series. Adding a lung term to `Xin_ve` would double-count.
          -  **Gut & Spleen**: They drain via portal vein to the liver first: `Xin_li = (Q_li - Q_sp - Q_g) * C_ar + Xout_g + Xout_sp`. Because the portal-drained organs (gut and spleen) pass through the liver first, their outflows are not added separately to `Xin_ve`.
            <img width="326" height="389" alt="Screenshot 2025-09-12 at 10 45 29 PM" src="https://github.com/user-attachments/assets/150e7694-d8a1-4618-9830-eafeff6b5cae" />
  
      - **Liver**: `Xin_li = (Q_li - Q_sp - Q_g) * C_ar + (Xout_g) + (Xout_sp)`
        -  `Q_li` is total hepatic flow. The liver has dual inflow - 1. hepatic artery carrying arterial blood, and 2. portal vein, which is exactly the outflow from gut and spleen. Thus writing blood flow as `Q_li − Q_sp − Q_g` avoids double-counting when Q_li is total hepatic flow.
        -  Thus `Xin_li` (liver inflow) = arterial component (`((Q_li - Q_sp - Q_g)) * C_ar`) + portal component (`Xout_g + Xout_sp`).
      - **Lung**: `Xin_lg = Q_lg * C_ve`
        - The blood that flows into the lung tissue is venous blood, not arterial blood (unlike other tissues). Thus `C_ve` is multiplied instead of `C_ar`. 
- **Mass out**
  - Basic structure of mass out equation (Xout_T): `Xout_T = Q_T * Cv_T` = `Xout_T = Q_T * C_T * RB * (1/Kp_T)`
    - Note: `Cv_T = C_T * RB * (1/Kp_T)` is derived above. 
    - This basic structure is directly applied to mass in equation of adipose, bone, brain, gut, heart, kidney, liver, lung, muscle, skin, and spleen.
    - The following tissues had slight variations in mass in equations:
      - **Artery**: `Q_lg * C_ar`
        - The artery is a compartment that delivers blood to all tissues (except for lung). The total arterial outflow equals the cardiac output (`Q_lg` ≡ `Q`) times the arterial blood concentration. 
        - Note: Artery is a blood pool, not a tissue. Therefore, the blood concentration `C_ar` is directly used (Kp applies in tissues, not in arterial blood).
      - **Vein**: `Q_lg * C_ve`
        - All tissue outflows merge into the mixed venous pool, which goes only to the lung. Therefore venous outflow equals lung inflow (`Xin_lg = Q_lg * C_ve`).



## Blood flow
- Blood flow of each tissue is determined by multiplying cardiac output and specific fraction (specific fraction can be found in literature or SimCYP).
  - e.g.
    - `Q = 80 ; cardiac output`
    - `Q_lg = Q ; lung`
    - `Q_a = Q * 5.9/100 ; adipose`
- **`Q_rest`** (blood flow of rest of body / residual tissue)
  - In PBPK models, the **cardiac output** (**Q**) is usually **larger** than the sum of blood flows assigned to explicitly modeled tissues (`ΣQ_T`). That’s because real organisms have many organs not included in the model (e.g., pancreas, thyroid, GI sub-organs, reproductive organs, skin appendages, etc.). 
  - **Rest of Body (ROB)** (also called *Residual tissue*) is a lumped compartment that collects the **unassigned** blood flow and tissue mass from all omitted organs.
  - To conserve **flow** and **mass**, the leftover flow must be routed somewhere, and it is done by defining a residual flow (`Q_rest`).
    - Define a residual flow: `Q_rest = Q − (Q_a + Q_bo + Q_b + Q_h + Q_k + Q_li + Q_m + Q_sk)`
    - What it does: With ROB, total inflow/outflow is balanced so that: `Σ all tissue flows + Q_rest = Q`. Lung inflow/outflow and venous/arterial pools remain consistent without artificially inflating any single tissue’s flow.
      - Note: Because `Q_li` represents total hepatic flow (hepatic artery + portal vein), the gut and spleen flows (`Q_sp` and `Q_g`) are already included in `Q_li`. Therefore, `Q_sp` and `Q_g` are not subtracted again from `Q` when calculating `Q_rest`.


## Weight
- Note that standard average weight of rat (250g) is used in this model. 


# Human IV Model
## Period setting
*Note: The period setting should be aligned with the literature conditions to ensure valid comparison.*

### **CODE**:
- `STARTTIME = 0` ; Simulation start time (min)
- `STOPTIME = 2890` ; Simulation end time (min) ; 10-min infusion + 2880-min post-infusion
- `DT = 0.001`; Solver integration step (min). Smaller → more accurate (slower); larger → faster but risk of error.
- `DTOUT = 5`; Output sampling interval (min). Results are recorded/shown every 5 min (doesn’t affect dynamics).

### Why `STOPTIME = 2890` when the study sampled for 2880 min?

The literature to compare used a **10-min IV infusion**, then collected samples for **2880 min post-infusion**.  
To reproduce this, the model runs for the **infusion (10 min) + sampling (2880 min) = 2890 min**:

- Simulate: `STARTTIME = 0`, `STOPTIME = 2890` (infusion occurs during 0–10 min).
- Analyze/plot on a **post-infusion clock** by realigning time:  
  - Treat the concentration at `t = 10 min` as `t′ = 0`.
  - Discard rows with `t′ < 0` (i.e., pre-infusion times after shifting).

This way, simulated times align exactly with the **post-infusion** sampling window reported in the literature.

## Administration
*Note: The administration setting should be aligned with the literature conditions to ensure valid comparison.*
### **CODE**:
- `dose_IV = 1000000   ;ng`
  - Defines the total IV dose in nanograms (ng).
- `dosing_time_IV = 10 ;min`
  - Defines the infusion duration in minutes.
- `IV_input = IF t< dosing_time_IV THEN dose_IV/dosing_time_IV ELSE 0`
  - Defines the infusion rate (ng/min) as a time-dependent input.
  - If the simulation time `t` is still within the infusion window (`t < dosing_time_IV`), drug is delivered at a constant rate (`Rate = Total dose / Infusion duration`)
  - Once infusion time is over (`t ≥ dosing_time_IV`), the input is set to 0, meaning no more drug enters the system.

## EP Calculation
This is the same as in what's discussed in rat IV model. Please refer to **'Rat IV Model - EP Calculation'** section.

## Vss Calculation
This is the same as in what's discussed in rat IV model. Please refer to **'Rat IV Model - Vss Calculation'** section.


## Predicted Human Kp values
As a heuristic cross-species adjustment, human Kp values were obtained by scaling rat Kp values by the plasma-unbound fraction (`fup`) ratio (`fup_human / fup_rat`).

## Metabolism & Excretion
### Renal Clearance
#### **CODE**:
- `GFR_human = 120 ;mL/min`
- `CL_r = (fup/RB * GFR_human) ;mL/min ; fub = fup/RB`
- `CL_r_u_human = GFR_human`
#### **Derivation**:
- Definitions
  - `CL_r_blood = elimination_rate / C_blood`
  - `CL_r_u_human = elimination_rate / C_unbound`
  - `C_unbound = fub * C_blood`
  - `fub = fup / RB`

- Filtration removes only UNBOUND drug:
  - `elimination_rate` = `C_unbound * GFR` = `(fub * C_blood) * GFR`

- Therefore (algebra):
  - `CL_r_blood` = `(fub * C_blood * GFR) / C_blood` = `fub * GFR`
  - `CL_r_u_human` = `(fub * C_blood * GFR) / (fub * C_blood)` = `GFR`

### **Renal Excretion**: 
#### **CODE**:
- `Xexc_r = CL_r_u_human * (C_k * (1/Kp_k)) * fup`
#### **Derivation**:

<img width="327" height="68" alt="Screenshot 2025-09-12 at 9 29 51 PM" src="https://github.com/user-attachments/assets/14f18d62-a625-4829-b64d-e77e34b469d5" />

- In this Mass balance differential equation of kidney tissue, the metabolism equation is `CL_r_u_human * Cv_k_u`.
- `Cv_k_u = Cv_k * fub` ; fub is multiplied to obtain unbound drug concentration in venous 'blood'.
  - `Cv_k = C_k * (1/Kp_k) * RB`
    - *Please refer to **Non-Eliminating Tissue Differential Equation Derivation** in **Rat IV Model - Differential Equation** section for the derivation of `Cv_k`.*
  - `fub = fup / RB`
- Thus `Cv_k_u` = `C_k * (1/Kp_k) * RB * (fup / RB)` = `C_k * (1/Kp_k)) * fup`
- Therefore, `Xexc_r = CL_r_u_human * (C_k * (1/Kp_k)) * fup`


### **CL_int_eff**: 
#### **CODE**:
- `CL_int_eff = 2710 ;mL/min`
  - Since `CL_int_eff = 2710` obtained from literature is already in the standard of whole blood concentration, there is no need to divide it by fu_MP - it is already scaled to in vivo. 

### **Hepatic Metabolism**: 
#### **CODE**:
- `Xmet_li = CL_int_eff * (RB * C_li * (1/Kp_li))`   
#### **Derivation**:
- Since `CL_int_eff` is already in the standard of whole blood concentration, there is no need to multiply `unbound Cv_LI` - just multiply `Cv_LI` value. 
  - `Cv_li = C_li * (1/Kp_li) * RB`
    - *Please refer to **Non-Eliminating Tissue Differential Equation Derivation** in **Rat IV Model - Differential Equation** section for the derivation of `Cv_li`.*
    - Again, there is no need to multiply `fub` (= `fup / RB`) as we are not solving for `Cv_li_u`.
      - *Note that this is valid only if CL_int_eff = 2710 represents a whole-liver, blood-standard intrinsic clearance estimated under steady-state conditions. It does not apply when distribution has not been fully achieved.*
- Therefore, `Xmet_li = CL_int_eff * (RB * C_li * (1/Kp_li))`

## **Differential Equations**: 
This is the same as in what's discussed in rat IV model. Please refer to **'Rat IV Model - Differential Equations'** section.

## Weight
- Note that standard average weight of male human (70kg = 70000g) is used in this model. 
- Since this human model did not require organ weights, they were not defined. If needed (e.g., when using microsomal intrinsic clearance and requiring liver weight for in vivo scaling), human organ weights can be obtained from the SimCYP human database.
- This can be adjusted as needed.

## Converting Output
- Since the literature reports drug concentration as venous plasma concentration (`Cp_ve`), the model should also provide output in terms of Cp_ve to align with the literature. As the current model is expressed in blood concentration, the venous blood concentration (`C_ve`) must be converted to `Cp_ve` using the blood-to-plasma ratio (`RB`): `Cp_ve = C_ve / RB`.


# Human PO Model

## Period setting
*Note: The period setting should be aligned with the literature conditions to ensure valid comparison.*
### **CODE**:
- `STARTTIME = 0` ; Simulation start time (min)
- `STOPTIME = 2880` ; Simulation end time (min) 
- `DT = 0.001`; Solver integration step (min). Smaller → more accurate (slower); larger → faster but risk of error.
- `DTOUT = 5`; Output sampling interval (min). Results are recorded/shown every 5 min (doesn’t affect dynamics).

## Administration
*Note: The administration setting should be aligned with the literature conditions to ensure valid comparison.*
### **CODE**:
- `dose_PO = 40000000 ;ng`
  - Defines the total PO dose in nanograms (ng). 

## EP Calculation
This is the same as in what's discussed in rat IV model. Please refer to **'Rat IV Model - EP Calculation'** section.

## Vss Calculation
This is the same as in what's discussed in rat IV model. Please refer to **'Rat IV Model - Vss Calculation'** section.

## Predicted Human Kp values
This is the same as in what's discussed in human IV model. Please refer to **'Human IV Model - Predicted Human Kp values'** section.

## Metabolism & Excretion
This is the same as in what's discussed in human IV model. Please refer to **'Human IV Model - Metabolism & Excretion'** section.

## Absorption
### **CODE**:
- `ka = 0.25/60 ; 1/h --> 1/min`
- `Fobs = 0.27`
- `FH = Q_li / (Q_li + CL_int_eff)`
- `FaFg = MIN(1, Fobs / FH)`       
- `INIT A_gut = dose_PO`
- `d/dt(A_gut) = -ka * A_gut`
- `Rabs0 = ka * A_gut ;ng/min`
- `Rabs = FaFg * Rabs0`

### **Derivation**:
- `ka = 0.25/60 ; 1/h --> 1/min`
  - In humans, ka (absorption rate constant) values observed in literature often fall within the ~0.1 to a few h⁻¹ range (e.g. ~0.2-1.0 h⁻¹ in many studies). A specific ka value should be selected through fitting, based on which estimate best reproduces key parameters such as AAFE, Tmax, and Cmax across multiple trial simulations. 

- `Fobs = 0.27`
  - This is bioavailability of propranolol reported by literature. 

- `FH = Q_li / (Q_li + CL_int_eff)`
  - Definition:
    - Hepatic Extraction ratio (EH): `EH = (Cin - Cout) / Cin` (fraction removed in a single pass through the liver)
    - Hepatic availability (FH): `FH = Cout / Cin`
      - `FH = 1 - EH` = `1 - ((Cin - Cout) / Cin)` = `(Cin / Cin) - ((Cin - Cout) / Cin)` = `Cout / Cin`
  - Mass balance equation (at steady state):
    - Input to liver (arterial blood inflow) − output from liver (venous blood outflow) = metabolised
    - `Q_li * (Cin - Cout) = CL_int_u * (fub * Cout)`
  - Rearrangement:
    - `Cin − Cout = (CL_int_u * fub * Cout) / Q_li`
    - `Cin` = `Cout + ((CL_int_u * fub * Cout) / Q_li)` = `((Q_li * Cout) + (CL_int_u * fub * Cout)) / Q_li` = `Cout * (Q_li + (CL_int_u * fub)) / Q_li`
    - `Cout / Cin` = `Cout / (Cout * (Q_li + (CL_int_u * fub)) / Q_li)` = `Q_li / (Q_li + (CL_int_u * fub))`
  - Thus, `FH` = `Cout / Cin` = `Q_li / (Q_li + (CL_int_u * fub))`
    - Since we have CL_int_eff from literature and `CL_int_eff = fub * CL_int_u`, `FH = Q_li / (Q_li + CL_int_eff)` and there is no need to multiply by `fub` again. 
  - Thus, `FH = Q_li / (Q_li + CL_int_eff)`

- `FaFg = MIN(1, Fobs / FH)`
  - `Fa * Fg` represents intestinal loss (where Fa = fraction absorbed in gut; Fg = fraction escaping gut-wall elimination).
  - Under linear PK, systemic oral bioavailability is `F_obs = Fa * Fg * FH`. 
  - Thus, `Fa * Fg = F_obs / FH`
  - Function `MIN(1,` is used to numerically cap to [0, 1] to avoid round-off/estimation artifacts.

- `INIT A_gut = dose_PO`
  - This states variable and initial condition.

- `d/dt(A_gut) = -ka * A_gut`
  - This reflects first-order depletion from the gut lumen.

- `Rabs0 = ka * A_gut ;ng/min`
  - This is uncorrected absorption flux into portal vein (pre-gut loss).

- `Rabs = FaFg * Rabs0`
  - Apply intestinal loss (`Fa * Fg`) to `Rabs0` (uncorrected absorption flux into portal vein) (post-gut loss) so that systemic `F_obs = FaFg * FH`.
  - Thus `Rabs` represents the amount that actually enters the portal vein after traversing the intestinal wall.


## **Differential Equations**: 
This is the same as in what's discussed in rat IV model. Please refer to **'Rat IV Model - Differential Equations'** section.


## Weight
This is the same as in what's discussed in human IV model. Please refer to **'Human IV Model - Weight'** section.



## Converting Output
This is the same as in what's discussed in human IV model. Please refer to **'Human IV Model - Converting Output'** section.

