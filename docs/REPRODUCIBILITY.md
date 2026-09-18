# Reproducibility

Run the EDA notebooks in numerical order, then the assessed notebook.

Core Python packages: pandas, numpy, matplotlib. The deeper EDA also uses statsmodels and scipy. KaggleHub is an optional dataset retrieval route.

The assessed notebook does not depend on the EDA notebooks for calculation; the EDA trail provides the audit history for insight selection.

Key safeguards:
- source rows retained; duplicate-removal only as sensitivity analysis;
- outcome fields are not used as explanatory predictors;
- partial-year coverage is disclosed;
- cancellation is not treated as realised revenue loss;
- observational associations are not presented as causal effects.
