# Model Derivation
- All equations in PBPK model were manually derived using the basic rationale discussed in the following research paper: https://doi.org/10.2165/00003088-200645050-00006.
- A physiologically based, perfusion-limited, well-stirred PBPK model was implemented for rat IV, human IV, and human PO simulations.
- All models are in the standard of blood concentration. Therefore, `fub (= fup / RB)` (unbound drug fraction in blood) is used to maintain the standard if needed.
  - Models may be built on plasma concentration, but the standard (blood vs. plasma) must remain consistent across the model.
    
# Parameters To Prepare
- Parameter values that are directly brought from literature or SimCYP include:
  - **Drug-specific parameters**:
    - fup (unbound drug fraction in plasma)
    - RB (ratio blood:plasma)
  - **Species-specific parameters**:
    - GFR (Glomerular Filtration Rate)
    - Tissue volume (V)
    - Blood flow (Q)
    - Weight (body weight & organ weight)
    - Hepatic IVIVE scaling factors
      - HPGL – hepatocytes per gram liver (cells/g liver)
      - MPPGL (or MPPGL_mic) – microsomal protein per gram liver (mg/g liver)
      - S9PGL – S9 protein per gram liver (mg/g liver)
  - **Species and drug-specific parameters**:
    - CL_int (intrinsic clearance)
    - ka (absorption rate constant)
    - Fobs (known/reported bioavailability)

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
code:
- `STARTTIME = 0` ; Simulation start time (min)
- `STOPTIME = 120` ; Simulation end time (min)
- `DT = 0.001`; Solver integration step (min). Smaller → more accurate (slower); larger → faster but risk of error.
- `DTOUT = 1`; Output sampling interval (min). Results are recorded/shown every 1 min (doesn’t affect dynamics).

## Administration
code:
- `dose_IV = 2500000 * BW/1000  ;ng ;(BW/1000=kg)`
  - Defines the total IV dose in nanograms (ng).
  - Because 2500000 is in the unit of ng/kg, body weight in kilograms (kg) must be multiplied to change the unit to ng. 
    - `BW/1000` converts body weight from grams (g) to kilograms (kg), since dosing is usually expressed per kg.
- `dosing_time_IV = 30/60 ;min`
  - Defines the infusion duration in minutes.
  - `30/60 = 0.5 min` means the infusion lasts 30 seconds
  - (Adjustable depending on whether you want bolus-like administration or longer infusion.)
- `IV_input = IF t< dosing_time_IV THEN dose_IV/dosing_time_IV ELSE 0`
  - Defines the infusion rate (ng/min) as a time-dependent input.
  - If the simulation time `t` is still within the infusion window (`t < dosing_time_IV`), drug is delivered at a constant rate (`Rate = Total dose / Infusion duration`)
  - Once infusion time is over (`t ≥ dosing_time_IV`), the input is set to 0, meaning no more drug enters the system.

## Predicted Kp values
Kp (tissue-to-plasma partition coefficient) values were obtained using standard partition coefficient calculators (Poulin–Theil): 

  <img width="578" height="327" alt="Screenshot 2025-09-15 at 1 51 55 PM" src="https://github.com/user-attachments/assets/1d280f9c-fe0e-4fa4-8c0f-007078901cff" />

## Metabolism & Excretion
### Renal Clearance
#### **CODE**:
- `GFR_rat = 18 ;ml/min`
- `CL_r = (fup/RB * GFR_rat) ;ml/mi ; fub = fup/RB`
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

### **Renal Metabolism**: 
#### **CODE**:
- `Xmet_r = CL_r_u * (C_k * (1/Kp_k)) * fup`
#### **Derivation**:

<img width="327" height="68" alt="Screenshot 2025-09-12 at 9 29 51 PM" src="https://github.com/user-attachments/assets/14f18d62-a625-4829-b64d-e77e34b469d5" />

- In this Mass balance differential equation of kidney tissue, the metabolism equation is `CL_R_u * Cv_k_u`.
- `Cv_k_u = Cv_k * fub` ; fub is multiplied to obtain unbound drug concentration in venous 'blood'.
  - `Cv_k = C_k * (1/Kp_k) * RB`
    - *Please refer to **Non-Eliminating Tissue Differential Equation Derivation** in **Rat IV Model - Differential Equation** section for the derivation of `Cv_k`.*
  - `fub = fup / RB`
- Thus `Cv_k_u` = `C_k * (1/Kp_k) * RB * (fup / RB)` = `C_k * (1/Kp_k)) * fup`
- Therefore, `Xmet_r = CL_r_u * (C_k * (1/Kp_k)) * fup`
#### Note:
Propranolol is almost completely hepatically metabolised, thus it is rational to put `Xmet_r` as 0. 

### **CL_int_u**: 
#### **CODE**:
- `CL_int = 0.13 * MPPGL_mic * W_li ;ml/min`
- `fu_MP = 0.49`
- `CL_int_u = CL_int / fu_MP`
#### **Derivation**:
- `CL_int = 0.13` is microsomal intrinsic clearance obtained from literature and is in the unit of ml/min/mg MP. `MPPGL_mic * W_li` is multiplied for in vivo scaling.
  - `MPPGL_mic`: mg microsomal protein / g liver.
  - `W_li`: liver weight (g).
  - Unit check: *(ml/min/mg) × (mg/g) × (g) = ml/min* → whole-liver intrinsic clearance.
- `fu_MP = 0.49` is unbound fraction in microsomal incubation.
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

- `VT * d/dt(C_T) = Q_T * C_ab - Q_T * Cv_T`
  - Mass in: `Q_T * C_ab`
  - Mass out: `Q_T * Cv_T`
  - There is no differential equation for Cv_T as blood outflow is different depending on the tissues. Therefore, the following conversion is used to define Cv_T:
    - `Kp = C_T / C_p` ; C_T = tissue concentration, C_P = plasma concentration
    - Thus `C_p = C_T / Kp`
    - `Cv_T = C_p * RB` ; RB is multiplied to convert the standard from plasma to blood concentration
    - Thus `Cv_T = (C_T / Kp) * RB`
  - Thus, non-eliminating tissue differential equation can be written again as:
    `VT * d/dt(C_T) = (Q_T * C_ab) - (Q_T * C_T / Kp * RB)`

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
      - **Kidney**: `d/dt(C_k) = (1/Vk) * (Xin_k - Xout_k - Xmet_r)`
        - To reflect renal clearance, `Xmet_r` is incorporated in the equation (because metabolised amount = `Xmet_r` is removed from total kidney concentration, Xmet_r is subtracted).
      - **Liver**: `d/dt(C_li) = (1/Vli) * (Xin_li - Xout_li - Xmet_li)`
        - To reflect hepatic metabolism, `Xmet_li` is incorporated in the equation (because metabolised amount = `Xmet_li` is removed from total liver concentration, `Xmet_li` is subtracted).
- **Mass in**
  - Basic structure of mass in equation `(Xin_T): Xin_T = Q_T * C_T`
    - This basic structure is directly applied to mass in equation of adipose, bone, brain, gut, heart, kidney, muscle, skin, and spleen.
    - The following tissues had slight variations in mass in equations:
      - **Artery**: `Xin_ar = Xout_lg`
        - `Xout_lg` = `Q_lg * Cv_lg` = `Q_lg * C_lg * RB * (1/Kp_lg)`
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
    - Define a residual flow: `Q_rest = Qco − (Q_a + Q_bo + Q_b + Q_h + Q_k + Q_li + Q_m + Q_sk)`
    - What it does: With ROB, total inflow/outflow is balanced so that: `Σ all tissue flows + Q_rest = Q`. Lung inflow/outflow and venous/arterial pools remain consistent without artificially inflating any single tissue’s flow.


## Weight
- Note that standard average weight of rat (250g) is used in this model. 


# Human IV Model

## Administration
code:
- `dose_IV = 1000000   ;ng`
  - Defines the total IV dose in nanograms (ng).
- `dosing_time_IV = 10 ;min`
  - Defines the infusion duration in minutes.
- `IV_input = IF t< dosing_time_IV THEN dose_IV/dosing_time_IV ELSE 0`
  - Defines the infusion rate (ng/min) as a time-dependent input.
  - If the simulation time `t` is still within the infusion window (`t < dosing_time_IV`), drug is delivered at a constant rate (`Rate = Total dose / Infusion duration`)
  - Once infusion time is over (`t ≥ dosing_time_IV`), the input is set to 0, meaning no more drug enters the system.

## Period setting
code:
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

## Predicted Human Kp values
Rat Kp values obtained above are converted to human Kp values by multiplying fup ratio (`fup_human / fup_rat`).


## Metabolism & Excretion
### Renal Clearance
#### **CODE**:
- `GFR_human = 120 ;mL/min`
- `CL_r = (fup/RB * GFR_human) ;ml/mi ; fub = fup/RB`
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

### **Renal Metabolism**: 
#### **CODE**:
- `Xmet_r = CL_r_u_human * (C_k * (1/Kp_k)) * fup`
#### **Derivation**:

<img width="327" height="68" alt="Screenshot 2025-09-12 at 9 29 51 PM" src="https://github.com/user-attachments/assets/14f18d62-a625-4829-b64d-e77e34b469d5" />

- In this Mass balance differential equation of kidney tissue, the metabolism equation is `CL_r_u_human * Cv_k_u`.
- `Cv_k_u = Cv_k * fub` ; fub is multiplied to obtain unbound drug concentration in venous 'blood'.
  - `Cv_k = C_k * (1/Kp_k) * RB`
    - *Please refer to **Non-Eliminating Tissue Differential Equation Derivation** in **Rat IV Model - Differential Equation** section for the derivation of `Cv_k`.*
  - `fub = fup / RB`
- Thus `Cv_k_u` = `C_k * (1/Kp_k) * RB * (fup / RB)` = `C_k * (1/Kp_k)) * fup`
- Therefore, `Xmet_r = CL_r_u_human * (C_k * (1/Kp_k)) * fup`
#### Note:
Propranolol is almost completely hepatically metabolised, thus it is rational to put `Xmet_r` as 0. 


### **CL_int_u**: 
#### **CODE**:
- `CL_int_eff = 2710 ;ml/min`
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
- This can be adjusted based on the need (e.g. if want to model propranolol behaviour in 50kg human, change the body weight and organ weights accordingly).

## Converting Output
- Since the literature reports drug concentration as venous plasma concentration (`Cp_ve`), the model should also provide output in terms of Cp_ve to align with the literature. As the current model is expressed in blood concentration, the venous blood concentration (`C_ve`) must be converted to `Cp_ve` using the blood-to-plasma ratio (`RB`): `Cp_ve = C_ve / RB`.


# Human PO Model

## Administration
code:
- `dose_PO = 40000000 ;ng`
  - Defines the total PO dose in nanograms (ng). 

## Period setting
code:
- `STARTTIME = 0` ; Simulation start time (min)
- `STOPTIME = 2880` ; Simulation end time (min) 
- `DT = 0.001`; Solver integration step (min). Smaller → more accurate (slower); larger → faster but risk of error.
- `DTOUT = 5`; Output sampling interval (min). Results are recorded/shown every 5 min (doesn’t affect dynamics).

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
  - ka in human is usually in the range of 0.06-6 (1/h). Specific ka (absorption rate constant) value must be selected (fitted) depending on which ka yields the data points that best-describe AAFE, Tmax, Cmax, etc.

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

