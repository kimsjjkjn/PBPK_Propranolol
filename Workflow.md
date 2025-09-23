# Workflow

## 1) Install Berkeley Madonna
- Open the official download page: https://berkeley-madonna.myshopify.com/pages/download (free software).
- Download and install the latest Berkeley Madonna that matches your machine (e.g., Windows, macOS Intel, Apple Silicon).

## 2) Run the models (Berkeley Madonna)

- Open Berkeley Madonna → **File ▸ New** → paste the full model code.  
  - If you want to use the code in this repository, open [Rat IV code](https://github.com/kimsjjkjn/PBPK_Propranolol/blob/main/code/Rat%20IV%20code), [Human IV code](https://github.com/kimsjjkjn/PBPK_Propranolol/blob/main/code/Human%20IV%20code), or [Human PO code](https://github.com/kimsjjkjn/PBPK_Propranolol/blob/main/code/Human%20PO%20code) on GitHub, click **Raw**, copy all, and paste.
  - The parameter values in these files are project-specific. Adjust them as needed for your use case.

- **Plot settings:** **Graph ▸ Choose Variables…** → set the Y-axis to `C_ar` or `Cp_ve`.
  - The Y-axis selected in the model should match the Y-axis reported in the literature for comparison. For example,  
    - If the literature reports **arterial blood** concentrations, plot `C_ar`.  
    - If it reports **venous plasma**, convert and plot `Cp_ve`.  
  - Always note the chosen matrix in the figure caption.  
  - *(Optional)* Use a log scale on the Y-axis for clearer display (**Graph ▸ Axis Settings…** → set Left Y Axis as auto and log).

- **Execute:** press **Run (▶)** → view results in **Table**.  
  - **Export results:** **File ▸ Export Table…** to save as CSV, or select all cells in **Table** and paste directly into Excel.

- **Save:** keep a copy of your model code; the **Table** output isn’t saved automatically, so export it separately.

## 3) Data Processing in Excel
- Paste the exported **Table** (predictions) into an Excel file.
- Add the literature in-vivo datasets in the same file if available.  
  - If raw in vivo time–concentration datasets from literature are unavailable, use digitised data based on the figures in the literature for plotting time-concentration profile and profile-level model performance evaluation.
- Plot time–concentration overlays.
  - Change y-axis to log-scale for better display.
- Calculate metrics (Fold Error (FE), Absolute Average Fold Error (AAFE)) and PK parameters (AUC, t½, CL, Vss, Cmax, Tmax, F).
    - **Vss** can be calculated from running code in Berkeley Madonna because the calculating code for Vss is already embedded in the code. To view `Vss` (or `Vss_b`, as appropriate) value, go to **Graph ▸ Choose Variables…** → add `Vss` or `Vss_b` to the Y-axis, run the simulation, and then open Table to read its value (units: mL). Copy this value into Vss (L) cell in Excel and convert the unit to liters by dividing by 1000.
      - Which one to use?
        - Use `Vss` (plasma-referenced) when literature concentrations are reported in plasma (e.g., your rat IV model).
        - Use `Vss_b` (blood-referenced) when literature concentrations are in whole blood (e.g., your human IV and PO models).
  - For the formulas used to compute each metric and PK parameter, see the Excel file titled **[PBPK_Propranolol_Data_Processing.xlsx](PBPK_Propranolol_Data_Processing.xlsx)** in this repository - click any relevant cell to view its underlying formula in the formula bar.
    - Check the comments as well for notes and further explanation.
