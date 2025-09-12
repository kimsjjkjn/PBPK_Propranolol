# Workflow

## 1) Install Berkeley Madonna
- Open the official download page: https://berkeley-madonna.myshopify.com/pages/download
- Download and install the latest Berkeley Madonna that matches your machine (e.g., Windows, macOS Intel, Apple Silicon).

## 2) Run the models (Berkeley Madonna)

- Open Berkeley Madonna → **File ▸ New** → paste the full model code.  
  - If you want to use the code in this repo, open `code/Rat IV code`, `code/Human IV code`, or `code/Human PO code` on GitHub, click **Raw**, copy all, and paste.
  - The parameter values in these files are project-specific; adjust them as needed for your use case.

- **Plot settings:** **Graph ▸ Choose Variables…** → set the Y-axis to `C_ar` or `Cp_ve`.  
  - Match the matrix reported in the reference. For example,  
    - If the literature reports **arterial blood** concentrations, plot `C_ar`.  
    - If it reports **venous plasma**, convert and plot `Cp_ve`.  
  - Always note the chosen matrix in the figure caption.  
  - *(Optional)* Use a log scale on the Y-axis for clearer display.

- **Execute:** press **Run (▶)** → view results in **Table**.  
  - **Export results:** **File ▸ Export Table…** to save as CSV, or select all cells in **Table** and paste directly into Excel.

- **Save:** keep a copy of your model code; the **Table** output isn’t saved automatically, so export it separately.

## 3) Data Processing in Excel
- Paste the exported **Table** (predictions) into an Excel file; add the literature in-vivo data in the same file if available.  
  - If raw time–concentration datasets from literature are unavailable, use digitised data based on the figures in the literature.
- Calculate metrics (Fold Error (FE), Absolute Average Fold Error (AAFE)) and PK parameters (AUC, t½, CL, Vss, Cmax, Tmax, F).
  - Fold Error (FE): `FE = max(pred, obs) / min(pred, obs)`
  - AAFE: `AAFE = 10^( mean( |log10(FE)| ) )`
  - PK params: AUC (linear trapezoid), Cmax/Tmax (from profile), t½ (terminal slope), CL and Vss (as applicable), F (PO only).
  - For the formulas and equations used to compute each metric and PK parameter, please refer to the uploaded Excel file in this repository.
- Plot time–concentration overlays.
  - Change y-axis to log-scale for better display.
