# Modeling Asthma Exacerbation Risk Using Environmental Data and Differential Equations

This project develops a mathematical framework for studying how changing environmental conditions may influence simulated asthma-related inflammation over time.

## Research Question

**How do the timing, magnitude, and duration of combined environmental exposure affect simulated asthma-related inflammation over time?**

## Overview

Daily PM2.5, ozone, temperature, and humidity measurements from the Fairfax County / Dulles, Virginia area during 2024 are normalized and combined into an environmental exposure index.

The exposure index is used as the forcing input to a nonlinear ordinary differential equation describing the balance between environmentally driven increases in inflammation and medication / natural recovery.

## Mathematical Model

The model is

```math
\frac{dI}{dt}
=
\alpha E(t)(1-I)
-
[\beta M+\gamma]I
```

where:

- $I(t)$ is normalized simulated inflammation
- $E(t)$ is environmental exposure
- $\alpha$ controls environmental response
- $\beta$ controls medication effectiveness
- $M$ is the normalized medication level
- $\gamma$ controls natural recovery

## Environmental Exposure Index

The normalized environmental variables are combined using

```math
E(t)
=
0.40P(t)
+
0.30O(t)
+
0.15T(t)
+
0.15H(t)
```

where $P(t)$, $O(t)$, $T(t)$, and $H(t)$ represent normalized PM2.5, ozone, temperature, and humidity.

The weights are preliminary modeling assumptions rather than clinically calibrated values.

## Analyses

The project includes:

- baseline simulation using real 2024 environmental measurements
- clean-air and high-exposure stress-test scenarios
- exposure magnitude experiments
- exposure duration experiments
- exposure timing experiments
- model-implied lag analysis
- parameter sensitivity analysis
- environmental-weight sensitivity analysis
- equilibrium and stability analysis
- structural identifiability analysis
- practical identifiability analysis
- synthetic parameter recovery
- robustness of parameter recovery to observational noise
- numerical validation of RK45 against an exact analytical solution

## Key Findings

### Environmental Data and Baseline Simulation

The final dataset contained **365 daily environmental observations** from 2024.

Using the observed environmental exposure trajectory, the model produced:

- mean environmental exposure: **0.425**
- mean simulated inflammation: **0.489**
- maximum simulated inflammation: **0.603**

These inflammation values are normalized model states, not measured clinical inflammation levels.

### Exposure Magnitude

For a controlled 7-day exposure event, increasing the normalized exposure magnitude increased both peak and cumulative simulated inflammation.

| Exposure Magnitude | Peak Inflammation | Excess Inflammation AUC |
|---:|---:|---:|
| 0.40 | 0.465 | 0.876 |
| 0.60 | 0.563 | 1.789 |
| 0.80 | 0.634 | 2.490 |

### Exposure Duration

At a fixed exposure level of 0.70, longer exposure events produced larger peak and cumulative responses.

| Duration | Peak Inflammation | Excess Inflammation AUC |
|---:|---:|---:|
| 1 day | 0.442 | 0.391 |
| 3 days | 0.526 | 1.051 |
| 7 days | 0.601 | 2.162 |
| 14 days | 0.619 | 3.950 |

### Temporal Response

The strongest model-implied correlation between environmental exposure and simulated inflammation occurred at a **2-day lag**, with a correlation of approximately **0.781**.

This is a property of the mathematical model and should not be interpreted as evidence that real biological inflammation necessarily peaks two days after exposure.

### Structural Identifiability

With constant medication level \(M\), the model depends on the medication-effect and natural-recovery parameters through the combined quantity

```math
\delta = \beta M + \gamma

## Repository Structure

```text
asthma-exacerbation-model/
├── README.md
├── requirements.txt
├── data/
│   ├── README.md
│   └── fairfax_environmental_data_2024.csv
├── notebooks/
│   ├── README.md
│   └── Asthma_Model_Final.ipynb
└── results/
    ├── figures/
    └── tables/
