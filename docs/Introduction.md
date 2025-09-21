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
