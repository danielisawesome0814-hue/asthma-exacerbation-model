# Environmental Data

This directory contains the processed environmental dataset used as input to the mathematical model.

## File

`fairfax_environmental_data_2024.csv`

The dataset contains **365 daily observations from 2024** with the following columns:

- `Date`
- `PM25`
- `Ozone`
- `Temperature`
- `Humidity`

The final dataset contains no missing values.

## Use in the Model

Each environmental variable is independently min-max normalized to the interval \([0,1]\).

The normalized variables are then combined into the environmental exposure index

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
