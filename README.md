# HRSR-Folded-Clutter-phase-data
Reproducibility materials for Hybrid Regularized Sparse Reconstruction (HRSR) for folded clutter mitigation, including pseudorandom phase sequences and supporting simulation data.


# HRSR-Folded-Clutter

Reproducibility materials for the Hybrid Regularized Sparse Reconstruction (HRSR) method for folded clutter mitigation.

This repository provides the pseudorandom initial-phase sequences used in the simulations and additional independent realizations for robustness verification.

## Phase Sequences

The initial phase sequence is generated according to

\[
\phi_m = 2\pi\,\mathrm{rand},
\]

where `rand` generates pseudorandom samples from a uniform distribution over \([0,1)\). Thus, the initial phases are modeled as uniformly distributed over \([0,2\pi)\).

The phase sequence is generated once at the beginning of a simulation and then kept fixed throughout the corresponding experiments. No phase sequence is re-generated or re-optimized for individual Monte Carlo trials or different simulation conditions.

The repository contains 31 phase realizations:

| File | Description |
|------|-------------|
| `pha_0` | The exact pseudorandom phase sequence used to generate the simulation results reported in the paper. |
| `pha_1`–`pha_30` | 30 independently generated pseudorandom phase sequences used for additional robustness verification experiments. |

For the additional verification experiments, each phase realization is fixed throughout the corresponding experiment. The other simulation and algorithmic parameters are kept unchanged.

## Purpose of the Additional Realizations

The additional 30 phase realizations are used to examine whether the reconstruction performance is sensitive to a particular pseudorandom phase realization.

The verification experiments compare the mutual coherence and reconstruction performance obtained with different phase realizations. The results show comparable reconstruction performance across the tested realizations, indicating that the reported performance is not specific to the particular phase sequence used in the main simulations.

Due to space limitations, the results for individual phase realizations are not presented separately in the manuscript.

## Reproducibility

`pha_0` is provided to enable reproduction and verification of the phase-coded waveform used in the main simulation results.

The additional sequences `pha_1`–`pha_30` are provided for independent verification of the robustness of the method with respect to the pseudorandom initial-phase realization.

All phase values are provided in radians.

## Citation

If you use the phase sequences or materials in this repository, please cite the corresponding paper:

> [Hybrid Regularized Sparse Reconstruction for Airborne Early-Warning Radar Using Inter-Pulse Phase-Coded Waveforms]  
> [Xiaojian Xu]  
> [IEEE ACCESS]  

