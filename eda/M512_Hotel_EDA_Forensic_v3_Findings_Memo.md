# M512 HOTEL — FORENSIC EDA v3 FINDINGS MEMO

## Status
Deep-dive EDA complete. Final explanatory notebook not yet frozen.

## What survived
- Overall cancellation rate: 37.04% (44,224/119,390).
- Top three market segments contribute 93.0% of all cancellations.
- Lead-time gradient survives hotel/year/month/segment checks and adjusted modelling.
- City-vs-Resort gaps for Groups and Offline TA/TO survive sensitivity checks.
- Recorded prior successful-booking history remains a strong reliability marker, with the source-definition caveat.

## New forensic discovery
Cancellation probability and operational damage are not equivalent.
- Canceled-status records: 43,017.
- Median cancellation notice: 56 days before arrival.
- Cancellations within 0–7 days of arrival: 5,135 (11.9% of Canceled-status records).
This means a high-cancellation segment may still give the hotel time to resell some inventory. Final recommendations should distinguish early cancellations, late cancellations, and no-shows.

## Important demotions
- Distribution channel is partly redundant with market segment; avoid presenting both as separate discoveries unless they add different decisions.
- Deposit type remains quality/process analysis only.
- Parking-space pattern remains quality/process analysis only.
- Booking changes remain unsuitable as a pre-booking intervention lever.
- ADR remains weak for the main story.

## Final candidate narrative
SCALE → RELIABILITY PROBABILITY → CONCENTRATION → HOTEL CONTEXT → CANCELLATION TIMING / OPERATIONAL HARM → RELIABILITY MARKERS → TARGETED ACTION

## Final methodological warning
The dataset is observational and anonymised, with no booking ID or realised-resale/revenue field. Do not claim causation, realised revenue loss, or that all cancellations have equal commercial impact.
