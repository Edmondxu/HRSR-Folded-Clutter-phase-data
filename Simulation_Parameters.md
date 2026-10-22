# Simulation Parameters

This file summarizes the simulation setup and parameter values reported in the manuscript *Hybrid Regularized Sparse Reconstruction for Airborne Early-Warning Radar Using Inter-Pulse Phase-Coded Waveforms*. Parameters that are not numerically specified in the manuscript are identified explicitly rather than inferred.

## 1. Platform and Radar Configuration

| Category | Parameter | Value |
|---|---|---|
| Platform | Flight altitude | 8,000 m |
| Platform | Flight speed | 150 m/s |
| Antenna | Aperture shape | Elliptical |
| Antenna | Major axis | 9 m |
| Antenna | Minor axis | 2 m |
| Radar | Frequency band | P-band |
| Radar | Carrier frequency | 450 MHz |
| Radar | Array pointing angle | 0° from the fuselage direction |
| Radar | Beam look angle | 45° from the fuselage direction |
| Platform motion | Assumption | Constant altitude and velocity |

## 2. Waveform and CPI Parameters

| Parameter | Value |
|---|---|
| Intra-pulse waveform | Linear frequency modulation (LFM) |
| Pulse width | 40 μs |
| Pulse repetition interval (PRI) | 240 μs |
| Waveform bandwidth | 5 MHz |
| Number of pulses, `M` | 128 |
| Number of Doppler grid points, `K` | `K = M = 128` |
| Derived CPI duration, `M × PRI` | 30.72 ms |
| Unambiguous range | 36 km |
| Doppler display | FFT-shifted, normalized Doppler in `[-0.5, 0.5)` |

### Inter-pulse phase sequence

The initial phase of each pulse follows the independent uniform phase model:

`phi_m ~ U(0, 2*pi)`, for `m = 0, ..., M-1`.

The original MATLAB generation rule is:

```matlab
2*pi*rand(Config.Npulse,1)
```

The phase sequence is generated once at the beginning of an experiment and kept fixed during that experiment.

- `pha_0`: the phase sequence used for the main simulation results (`M = 128`).
- `pha_1`–`pha_30`: 30 additional independently generated phase sequences used for robustness checks.

The phase-sequence files are available in the public repository:

<https://github.com/Edmondxu/HRSR-Folded-Clutter-phase-data>

## 3. Clutter Configuration

| Parameter | Value |
|---|---|
| Clutter model | Morchin model |
| Terrain | Hilly terrain |
| Maximum simulated clutter range | 330 km |
| Unambiguous range | 36 km |
| Range-folded regions included in the clutter model | `q = 0, 1, ..., 9` (10 regions) |

For HRSR, the clutter prior is obtained from a Capon Doppler spectrum estimated using neighboring range cells. For each cell under test:

- Candidate training cells: neighboring `±40` range cells.
- Guard cells excluded from training: `±3` range cells around the cell under test.

## 4. Target Configuration

The five target entries below follow the order reported in the manuscript's simulation-parameter table.

| Target | Range (km) | Velocity (m/s) | SCR (dB) | SNR (dB) |
|---:|---:|---:|---:|---:|
| 1 | 11 | -500 | -44.1 | 27.4 |
| 2 | 156 | 380 | -45.6 | 25.9 |
| 3 | 202 | -250 | -46.4 | 25.1 |
| 4 | 244 | 150 | -48.9 | 22.6 |
| 5 | 340 | 70 | -50.6 | 20.9 |

## 5. Reconstruction and Regularization Settings

| Method or setting | Value / rule reported in the manuscript |
|---|---|
| Conventional `l1`-regularized reconstruction | `lambda_1 = 14` |
| Elastic-net reconstruction | `lambda_e = 10`, `delta = 0.7` |
| HRSR | `lambda_n = 8`, `lambda_c = 1` |
| Regularization-parameter selection criterion | Grid search minimizing the absolute deviation between estimated residual power and the theoretical noise floor |
| FISTA implementation | FISTA with backtracking line search |
| Stopping rule | Relative change between successive iterates, with a maximum iteration limit |
| Backtracking | Step size reduced using the backtracking parameter |

The manuscript describes the FISTA parameters using the symbols `gamma_0`, `kappa`, `eta`, `I_max`, and `H_max`, but does not report their numerical values or the full grid-search ranges and resolutions. These values should be documented from the exact code version used to produce the results before claiming complete code-level reproducibility.

## 6. Computational Environment for Runtime Measurements

| Parameter | Value |
|---|---|
| CPU | Intel Core Ultra 7 265K, 20 cores |
| RAM | 32 GB |
| Operating system | Windows 10 Pro (64-bit) |
| MATLAB version | R2022b |
| Numerical precision | Double precision |
| MATLAB threading | Single-threaded implementation |
| GPU | Not used for the reported runtime measurements |

## 7. Random Seeds and Data Reproducibility

The exact phase-code realizations used in the main experiment and the additional phase-code checks are provided as files in the repository, so the phase sequence does not need to be regenerated to reproduce those experiments.

The manuscript does not specify random-seed values for every stochastic component of clutter and noise generation. For exact regeneration of those realizations, the corresponding seed values or the generated clutter/noise data should be archived alongside the simulation scripts. Seed values should be taken from the actual code and data-generation workflow rather than reconstructed or guessed.

## 8. Repository

Phase-sequence repository:

<https://github.com/Edmondxu/HRSR-Folded-Clutter-phase-data>

This document records the simulation parameters available from the manuscript. For full executable reproducibility, the numerical values of any implementation-specific solver settings and the random seeds or stored realizations used for clutter/noise generation should also be included with the corresponding code and data.
