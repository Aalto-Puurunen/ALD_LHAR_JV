# ALD_LHAR_JV — Example demo
Version: 1.8.1
This repository contains a single Python script that solves the 1D diffusion–reaction equations for ALD in a rectangular lateral high-aspect-ratio (LHAR) cavity using SciPy’s solve_ivp with the BDF method. Parameters are provided in an Excel workbook; results are written to a new Excel workbook in the same folder, and several diagnostic plots are displayed.

Acknowledgements: GENESIS project (Grant Agreement no. 101194246), Chips JU and its members, including top-up funding by Business Finland.

## What this demo provides
- A minimal, reproducible example parameter file and a one-command run
- Typical runtime and tested hardware
- Exact description of required inputs and the produced outputs

## Files
- ALD_LHAR_JV.py — main script (version 1.8.1; dated April 21, 2026)
- Parameters_ALD_LHAR.xlsx — input parameters workbook (sheet: LHAR_Parameters)
- Output: <RunningCode>_results.xlsx (written to the same directory)

## Requirements
- Python 3.12 and newer
- Packages:
-- numpy
-- scipy
-- pandas
-- matplotlib
-- openpyxl

Create an environment and install:
```
py -3.12 -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -U pip
pip install numpy scipy pandas matplotlib openpyxl
```
Optionally, write a requirements.txt with:

numpy
scipy
pandas
matplotlib
openpyxl

Install with pip install -r requirements.txt.

### NOTE
You can run this script in any environment that executes Python code—terminal/command line, IDEs (e.g., Spyder, VS Code, PyCharm), or Jupyter notebooks—provided Python 3.12 and the required packages (numpy, scipy, pandas, matplotlib, openpyxl) are installed in that environment. Ensure the working directory contains ALD_LHAR_JV.py and Parameters_ALD_LHAR.xlsx (sheet name: LHAR_Parameters), and close the Excel file before running. If running in a headless environment (no display), set the Matplotlib backend via MPLBACKEND=Agg to suppress GUI windows.

# Input workbook format
Place an Excel file named Parameters_ALD_LHAR.xlsx in the same folder as the script. It must contain a sheet named LHAR_Parameters. The script reads specific cells in column B:

B1 Running code (string; used as output filename prefix)
B3 Cavity height, H (m) float
B4 Cavity width, W (m) float
B5 Aspect ratio, AR (-) float; L/H
B6 Sticking probability, c (-) float
B7 Desorption probability, Pd (1/s) float
B8 Adsorption capacity, q (m-2) float
B9 Pulse time, t_pulse (s) float
B10 Temperature, T (K) float
B11 Partial pressure of reactant at z=0, pA0 (Pa) float
B12 Partial pressure of inert gas, pI (Pa) float
B13 Molar mass of reactant, MA (kg/mol) float
B14 Molecular diameter of reactant, dA (m) float
B15 Molar mass of inert gas, MI (kg/mol) float
B16 Molecular diameter of inert gas, dI (m) float
B17 Number of spatial grid points, Nx integer (>2)
B18 Number of time grid points, Nt integer (>1)
B19 Additional θ value for reporting penetration depth and slope (-) float in (0,1); if outside, script resets to 0.45
Important:

Close the Excel file before running (Windows/Excel locks the file).
Units must be exactly as noted.
Nx and Nt must be integers; set by formatting cells as “Number” with no text.
A minimal example (as shown in the screenshot) uses:

H = 5.00E-07 m, W = 0.01 m, AR = 1000, c = 1.0e-3, Pd = 0, q = 4.00E+18 m-2,
t_pulse = 0.5 s, T = 573 K, pA0 = 50 Pa, pI = 450 Pa,
MA = 0.072 kg/mol, dA = 6.00E-10 m, MI = 0.028 kg/mol, dI = 3.60E-10 m,
Nx = 500, Nt = 200, additional θ = 0.43,
Running code, e.g., Example_LHAR_001.
Running the demo
Ensure Parameters_ALD_LHAR.xlsx exists and is closed.
Run:

python ALD_LHAR_JV.py
The script will:

Solve the coupled system using solve_ivp(..., method='BDF')
Display several Matplotlib plots during execution
Write results to <RunningCode>_results.xlsx in sheet LHAR results
Print total runtime
Example output filename for the provided parameters: Example_LHAR_001_results.xlsx.

Typical runtime:

~3.7 s wall-clock
Tested on a machine with 32 GB RAM, 1.30 GHz CPU (CPU-only)
You can measure timing with:


/usr/bin/time -p python ALD_LHAR_JV.py
What the script computes
Geometry, transport, and regime indicators:
L, h, vA, DKn, DA, Deff, Knudsen number, Thiele modulus
PDE solution:
Partial pressure pA(x,t) and surface coverage θ(x,t) over x∈[0,L] and t∈[0, t_pulse]
Final-time profiles:
pA(x, t_final), θ(x, t_final), growth q·θ(x)
Penetration depth and slope:
x and x/H at θ targets [0.9 … 0.1] plus the additional θ in B19
PD at 50% coverage (x/H at θ=0.5), slope at θ=0.5, and back-extracted c (free molecular flow)
Output workbook structure
File: <RunningCode>_results.xlsx, sheet: LHAR results

The script writes four blocks:

Parameters (starting at A1):

Two columns: “Parameter”, “Value” with the exact inputs read from the Excel sheet
Includes script name and version, and the running code used as label
Calculated Values (starting at A23):

“Calculated Values”, “Value”
Includes L, h, vA, DKn, DA, Deff, Knudsen, Thiele, Δθ around 0.5, PD50 (m), PD50 (x/H), slope at 0.5, back-extracted c, exposure, and integrals:
Θ integral, ∫θ(x)dx (μm)
Growth integral, ∫Growth(x)dx (atoms·μm/nm²)
Final profiles data table (starting at E1):

Columns:
x (m)
x/H (-)
pA (Pa)
theta (-)
Growth (atoms/nm2) [note: “nm2” in header; values = q·θ converted to atoms/nm²]
Penetration-depth table (starting at J1):

Columns:
Theta (-)
x (m)
x/H (-)
Slope (-) [|dθ/d(x/H)| near the crossing]
Diff. in theta points (%) [local θ difference between adjacent grid points]
Number formats:

The script sets number formats ‘0.0000’ for columns H and I in the worksheet (Excel-only formatting).
Plots shown during the run:

Contour of pA(x,t)
Contour of θ(x,t)
Line plots at t_final for pA vs x, θ vs x, growth vs x
Corresponding plots versus x/H
These plots are displayed but not saved to disk.

Reproducibility notes
Solver: scipy.integrate.solve_ivp with method='BDF'
Deterministic given fixed inputs and grid (no randomness)
Grid:
Space: uniform grid with Nx points from 0 to L
Time: linear spacing of Nt points from 0 to t_pulse, passed as t_eval
Boundary conditions:
Pinned pA(0,t) = pA0 via initial condition and dPAdt[0] = 0
Neumann at outlet implemented by one-sided second derivative at x=L
Report exact library versions if needed:


python -V
python -c "import numpy,scipy,pandas,matplotlib; print('numpy',numpy.__version__); print('scipy',scipy.__version__); print('pandas',pandas.__version__); print('matplotlib',matplotlib.__version__)"
Troubleshooting
File locked or permission error:
Close Parameters_ALD_LHAR.xlsx in Excel before running.
KeyError: 'LHAR_Parameters':
Ensure the sheet is named exactly LHAR_Parameters.
Type errors (e.g., cannot convert string to float):
Ensure B3–B19 contain numeric values (no units or text).
Grid too small:
Ensure Nx ≥ 3 and Nt ≥ 2. Larger grids increase runtime and memory.
Solver convergence issues:
Extremely stiff settings or inconsistent units can cause failures. Verify units and consider reducing Nx or adjusting pulse time as a quick diagnostic.
Output filename confusion:
The saved file is <RunningCode>_results.xlsx even though the console message mentions _simulation_results.xlsx.
How to cite
Please cite the software and the paper:

Software: add your preferred software citation or DOI (e.g., Zenodo) here.
Model reference: Ylilammi et al., J. Appl. Phys. 123, 205301 (2018). https://doi.org/10.1063/1.5028178
License
Please add your software license here (e.g., MIT/Apache-2.0/GPL-3.0).
