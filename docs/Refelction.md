# Reflection
This independent project on physiologically based pharmacokinetic (PBPK) modeling of propranolol was conducted using Berkeley Madonna, with all organ-level differential equations derived from first principles. By constructing and validating rat (IV) and human (IV and PO) models, I developed hands-on experience in mechanistic model building, parameterization, and quantitative evaluation of model performance.

The project successfully validated the rat IV and human PO models, while also identifying key limitations in the human IV model and outlining directions for refinement. As a first attempt at PBPK modeling, the models were quite simplified. Therefore, future improvements including incorporating gastric emptying and intestinal transit into the oral absorption module and integrating transporter and enzyme dynamics should be done to reflect more complex in vivo mechanism.

Beyond the technical implementation, this project strengthened my understanding of PBPK mechanisms, provided practice in complete ODE derivation, and reinforced systematic model validation using fold-error metrics (FE, AAFE, within 2×/3×). Importantly, it highlighted both the strengths and challenges of PBPK modeling: exposure-based parameters can be reproduced with reasonable accuracy, but shape-dependent outcomes such as Tmax and terminal half-life require greater physiological complexity.

Overall, this work served as both a validated case study and a foundation for future extensions toward clinically predictive PBPK modeling.
