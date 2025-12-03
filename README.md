# InjMoldSimulation
This repository is a version of the original krebeljk/openInjMoldSim project adapted to OpenFOAM v2406 and simplified the viscosity model to significantly reduce computational time. ONLY FOCUS ON FILL STAGE!
![animation](https://github.com/user-attachments/assets/48a48444-3483-493c-a74e-7936ddf3edb4)

# ABOUT THE PROJECT

The original project simulates all stages of plastic injection molding (filling - holding - packing) with high accuracy and detailed using Compressible Cross-WLF model. However, It takes quite much times to simulate it due to complication of this solver who works on openFOAM version 7. (It takes 4-5 days depends on your PC.)

This repository handle the problems with three basic changes:

1. OpenFOAM version update for project;
Project has moved OpenFOAM version 2406.

2. Focused on first stage;
It only focuses on the filling phase, which has more value in reality.
 
3. Simplified of viscosity model;
The original Cross-WLF (non-Newtonian) viscosity model was simplified to a Williams-Landel-Ferry (WLF) (Newtonian assumption) or constant Newtonian viscosity model that is independent of speed and shear rate and depends only on temperature. This simplification enabled fast results, especially in early-phase (filling) simulations.

# Why Were These Changes Made?

Computation Speed: Calculating non-Newtonian viscosity (especially Cross-WLF) based on the shear rate at each iteration significantly increases simulation time. While the Newtonian assumption reduced the filling time from 4-5 days in the original project, this project reduced it to an acceptable time of only 2-3 hours (depends on your PC).

Version Compatibility: Migrating from OpenFOAM v7 to OpenFOAM v2406 allows the use of modern library and solver features.

Early Stage Analysis: This simplified model is ideal for early design stages, such as rapid preliminary analyses, mesh quality testing, and approximate filling time estimation.

# FUNCTIONALITY
- Compressible, non-isothermal, laminar cavity flow
- Tait equation of state
- WLF viscosity model
- Pure polymer melt flow only

# RESOURCES

- https://github.com/krebeljk/openInjMoldSim
- Krebelj, K., Krebelj, A., Halilovič, M., & Mole, N. (2021). Modeling Injection Molding of High-Density Polyethylene with Crystallization in Open-Source Software. Polymers, 13(1), 138.
- https://www.researchgate.net/publication/341807768_Verification_and_Validation_of_openInjMoldSim_an_Open-Source_Solver_to_Model_the_Filling_Stage_of_Thermoplastic_Injection_Molding

# Why Standard compressibleInterFoam is Inadequate for Industrial Plastic Injection Filling:

The standard compressibleInterFoam solver lacks critical physical models required to accurately simulate the filling phase of the plastic injection molding process:

1. Absence of Viscous Dissipation (Shear Heating): The default energy equation in OpenFOAM accounts only for convective and conductive heat transfer. It fails to model shear heating—the significant temperature rise caused by internal friction as the high-viscosity polymer flows through narrow gates and runners at high shear rates.

Consequence: The simulation predicts premature cooling and solidification (frozen flow), often resulting in false "short shots," whereas in reality, the shear heat would keep the melt fluid enough to fill the cavity.

2. Limited Rheological Modeling: Standard library models (like Bird-Carreau) do not natively support the full Pressure-Volume-Temperature (PVT) dependencies found in industrial standards like the Cross-WLF model.

Consequence: Without accounting for the pressure-dependence of viscosity, the solver cannot accurately predict the injection pressure requirements or the exact progression of the flow front under high-pressure conditions.
