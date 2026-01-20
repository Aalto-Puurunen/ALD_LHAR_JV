# ALD_LHAR_JV
Version: 0.6.1

Diffusion-reaction model for ALD on lateral high aspect ratio structures.

## Project description
This Python script provides the solution of the one-dimensional diffusion equation with surface reaction for partial pressure and surface coverage as function of time (Eqs. 10 and 16 of Ylilammi et al., J. Appl. Phys. 123, 205301, 2018, DOI: [10.1063/1.5028178](https://doi.org/10.1063/1.5028178)). Ylilammi's approximation to the diffusion equation is not used in this script. Instead, the partial differential equations for diffusion and reaction are solved numerically. For the surface reaction, the model uses Langmuir adsorption and includes a desorption term. For the calculations, the effective diffusion coefficient is assumed to be constant along the structure. This script can be used in a wide range of diffusion regimes (Kn number from Kn<<1 to Kn>>1). The script was written by Dr. Jorge A. Velasco, by request of Prof. Riikka L. Puurunen (Catalysis Group, Aalto University) with funding provided by the Genesis EU project (Chips JU, Horizon Europe).  

## Usage
The parameters for the simulation are entered in the accompanying file “Parameters_ALD_LHAR.xlsx”. The simulation is performed by running “ALD_LHAR_JV_v06-1.py”. There’s no need to modify the Python script nor the name of the parameters file. Once the simulation ends, the script creates a simulation results file (the given running code/name in the parameters file is shown in the result’s file name: “given running code”_simulation_results.xlsx). The simulation results file includes parameters, calculated values, final profiles for pressure and surface coverage along distance and distance divided by channel height.Calculated values include: diffusion coefficients, Knudsen number, Thiele modulus, penetration depth and slope at half coverage, and the back-extracted sticking coefficient for Kn >> 1 (as in Arts et al. J. Vac. Sci. Technol., A 37, 030908, 2019, DOI: [10.1116/1.5093620](https://doi.org/10.1116/1.5093620)).     

## Citing 
Please cite as:
J.A. Velasco and R. L. Puurunen, ALD_LHAR_JV – Diffusion-reaction model for ALD on lateral high aspect ratio structures, (2026), Github repository, [https://github.com/Aalto-Puurunen/ALD_LHAR_JV](https://github.com/Aalto-Puurunen/ALD_LHAR_JV) 

## Copyright and license
MIT License
Copyright 2026 (c) Jorge A. Velasco and Riikka L. Puurunen, Aalto University

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
