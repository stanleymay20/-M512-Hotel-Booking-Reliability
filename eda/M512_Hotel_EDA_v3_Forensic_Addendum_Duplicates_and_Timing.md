# M512 Hotel EDA v3 — Forensic Addendum: Duplicate Ambiguity and Cancellation Timing

## Status

This addendum corrects and sharpens the v3 deep-dive interpretation before any final insight freeze.

## 1. Exact duplicate-looking rows are a MATERIAL structural ambiguity

The source file has no unique booking identifier. Therefore exact repeated rows cannot safely be labelled as erroneous duplicates. They may represent multiple bookings with identical recorded attributes, especially block/group reservations.

However, a sensitivity test shows that the duplicate-handling decision materially changes several magnitudes:

| Metric | Full source rows | After `drop_duplicates()` |
|---|---:|---:|
| Rows | 119,390 | 87,396 |
| Overall cancellation | 37.0% | 27.5% |
| 0–7 day lead cancellation | 9.6% | 8.4% |
| 366+ day lead cancellation | 67.7% | 40.9% |
| Groups cancellation | 61.1% | 27.0% |
| Top-three share of cancellations | 93.0% | 91.8% |
| Prior-success recorded: cancellation | 5.5% | 5.0% |
| No prior success recorded: cancellation | 38.0% | 28.4% |
| ≥1 special request: cancellation | 21.7% | 21.7% |
| No special request: cancellation | 47.7% | 33.2% |

This means the **direction** of several findings survives, but the **magnitude** is sensitive.

### Where duplicate-looking rows concentrate

- Rows belonging to an exact-duplicate group: 40,165 (33.6% of all rows).
- **Groups:** 84.4% of rows belong to duplicate groups.
- **Offline TA/TO:** 50.4%.
- **Non Refund:** 98.1%.
- **366+ day lead time:** 90.5%.
- Some exact row groups contain very large repeated blocks, consistent with the possibility of group/block reservations.

### Decision for the assessed project

Use the **source rows as the primary booking population**, because there is no documented booking ID or evidence that exact repeated rows are accidental duplicates. Do **not** silently deduplicate.

But disclose this limitation explicitly and report that sensitivity analysis changes magnitudes substantially. Avoid language implying the exact percentages are invariant to duplicate handling.

## 2. Hotel × segment findings also shrink under deduplication

**Groups**
- Full: City 68.9% vs Resort 42.4%.
- Deduplicated sensitivity: City 33.8% vs Resort 19.3%.

**Offline TA/TO**
- Full: City 42.8% vs Resort 15.2%.
- Deduplicated sensitivity: City 17.3% vs Resort 12.1%.

The hotel-direction remains, but the effect sizes are smaller. This should be framed as **contextual heterogeneity**, not a fixed causal effect.

## 3. Cancellation timing changes the managerial story

There are 43,017 records with `reservation_status = Canceled`.

- Median cancellation notice: **56 days before arrival**.
- Cancellations within 0–7 days of arrival: **5,135 (11.9%)**.
- No-shows: **1,207**.

Therefore, **cancellation probability is not the same as operational harm**. A high-risk booking that cancels months ahead may leave time to resell inventory; a lower-volume late cancellation or no-show may be more operationally disruptive.

### Arrival-proximate failures (late cancellation within 7 days + no-show)

| market_segment   | late_cancel_0_7 | no_show | arrival_prox_fail | share_pct |
|:-----------------|-----------------:|--------:|------------------:|----------:|
| Online TA        | 2397 | 591 | 2988 | 47.1 |
| Offline TA/TO    | 751 | 231 | 982 | 15.5 |
| Groups           | 840 | 74 | 914 | 14.4 |
| Direct           | 645 | 212 | 857 | 13.5 |
| Corporate        | 394 | 76 | 470 | 7.4 |
| Complementary    | 69 | 12 | 81 | 1.3 |
| Aviation         | 37 | 11 | 48 | 0.8 |

**Online TA alone contributes 47.1% of these arrival-proximate failures.**

This suggests the final project should distinguish:
1. **probability of cancellation**, and
2. **timing/severity of booking failure**.

## 4. Revised freeze policy

### Strong enough to keep
- Cancellation burden as scale/context.
- Lead-time association, but with duplicate-sensitivity disclosure.
- Concentration of cancellation volume in major market segments.
- Hotel × segment heterogeneity, with sensitivity caveat.
- Recorded prior successful-booking history, with source-definition caveat.

### Newly elevated
- **Cancellation timing / arrival-proximate failure** as a potentially stronger operational insight than raw cancellation rate alone.

### Still reserve / quality-only
- Special requests: engagement marker, not causal lever.
- Distribution channel: highly overlapping with market segment.
- Deposit type: process/coding investigation.
- Parking: process/data-quality investigation.
- ADR-based value proxies: not realised revenue loss.

## 5. Forensic conclusion

The final explanatory notebook should not tell the simplistic story:

> “Long-lead Group bookings are the problem.”

A stronger, more defensible story is:

> **Booking failure has two dimensions: likelihood and timing. Long-lead and certain segment profiles are less reliable, while late cancellations and no-shows create a distinct arrival-proximate operational risk. Management should investigate targeted controls using both dimensions rather than relying on cancellation rate alone.**

This is a better consultancy story and a stronger critical-evaluation position.
