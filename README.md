# M512 Hotel Booking Reliability

A reproducible data-visualisation consultancy project using the **Hotel Booking Demand** dataset.

## Project question

Where does hotel booking failure concentrate, and how should management distinguish **cancellation likelihood** from **failure close to arrival**?

## Main assessed notebook

[Open the assessed notebook](https://github.com/stanleymay20/-M512-Hotel-Booking-Reliability/blob/main/analysis/M512_Hotel_Assessed_Draft_v0_3_GITHUB_LINKED.ipynb)

## Forensic EDA trail

1. [EDA v1 — structure, quality and broad screening](https://github.com/stanleymay20/-M512-Hotel-Booking-Reliability/blob/main/eda/M512_Hotel_EDA_Forensic_v1.ipynb)
2. [EDA v2 — robustness, source semantics and multivariable checks](https://github.com/stanleymay20/-M512-Hotel-Booking-Reliability/blob/main/eda/M512_Hotel_EDA_Forensic_v2.ipynb)
3. [EDA v3 — deep duplicate/timing investigation](https://github.com/stanleymay20/-M512-Hotel-Booking-Reliability/blob/main/eda/M512_Hotel_EDA_Forensic_v3_DEEP_DIVE.ipynb)
4. [v3 findings memo](https://github.com/stanleymay20/-M512-Hotel-Booking-Reliability/blob/main/eda/M512_Hotel_EDA_Forensic_v3_Findings_Memo.md)
5. [duplicate/timing addendum](https://github.com/stanleymay20/-M512-Hotel-Booking-Reliability/blob/main/eda/M512_Hotel_EDA_v3_Forensic_Addendum_Duplicates_and_Timing.md)

## Method

The repository deliberately separates **exploratory analysis** from **explanatory communication**. The assessed notebook recalculates every displayed statistic and remains self-contained; the EDA files document how candidate findings were tested and selected.

## Dataset

Kaggle: https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand

Antonio, N., de Almeida, A. and Nunes, L. (2019) ‘Hotel booking demand datasets’, *Data in Brief*, 22, pp. 41–49.

## Important analytical boundary

The data are observational. Recommendations are framed as priorities for investigation and testing, not causal prescriptions. Source rows are retained because there is no unique booking identifier; duplicate removal is treated as sensitivity analysis.