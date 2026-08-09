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

Controlled exposure experiments showed that greater exposure magnitude produced larger peak and cumulative simulated inflammation responses.

Longer exposure events also produced larger cumulative inflammation responses.

The strongest model-implied exposure-inflammation correlation occurred at a lag of approximately 2 days.

Structural identifiability analysis showed that, when medication is constant, the parameters $\beta$ and $\gamma$ cannot be estimated separately because the model depends on them through

```math
\delta = \beta M + \gamma
```

Synthetic parameter-recovery experiments therefore estimate the reduced parameters $\alpha$ and $\delta$.

Parameter-recovery accuracy decreased substantially under larger simulated observational noise.

The RK45 numerical implementation was validated against an exact constant-exposure solution and produced extremely small numerical error.

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
