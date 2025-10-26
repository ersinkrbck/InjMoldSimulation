# InjMoldSimulation
This repository is a version of the original krebeljk/openInjMoldSim project adapted to OpenFOAM v2406 and simplified the viscosity model to significantly reduce computational time.

ABOUT THE PROJECT

The original project simulates all stages of plastic injection molding (filling - holding - packing) with high accuracy and detailed using Compressible Cross-WLF model. However, It takes quite much times to simulate it due to complication of this solver who works on openFOAM version 7. (It takes 4-5 days depends on your PC.)

This repository handle the problems with two basic changes:

1. OpenFOAM version update for project;
Project has moved OpenFOAM version 2406.

2. Focused on first stage;
It only focuses on the filling phase, which has more value in reality.
 
3. Simplified of viscosity model;
The original Cross-WLF (non-Newtonian) viscosity model was simplified to a Williams-Landel-Ferry (WLF) (Newtonian assumption) or constant Newtonian viscosity model that is independent of speed and shear rate and depends only on temperature. This simplification enabled fast results, especially in early-phase (filling) simulations.

Why Were These Changes Made?

Computation Speed: Calculating non-Newtonian viscosity (especially Cross-WLF) based on the shear rate at each iteration significantly increases simulation time. While the Newtonian assumption reduced the filling time from 4-5 days in the original project, this project reduced it to an acceptable time of only 2-3 hours (depends on your PC).

Version Compatibility: Migrating from OpenFOAM v7 to OpenFOAM v2406 allows the use of modern library and solver features.

Early Stage Analysis: This simplified model is ideal for early design stages, such as rapid preliminary analyses, mesh quality testing, and approximate filling time estimation.


