# Data Quality Report
**AIRMAN Aeronautics — Skynet + TOGA Data Assessment**
Generated: 2026-05-15

---

## Summary

| Dataset | Rows | Columns | Issues Found |
|---------|------|---------|--------------|
| sorties.csv | 12 | 13 | Multiple |
| aircraft.csv | 3 | 7 | High defect flags |
| cadets.csv | 3 | 7 | Clean |
| instructors.csv | 3 | 6 | Clean |
| toga_study.csv | 5 | 8 | Missing cadets |
| payments.csv | 3 | 6 | Clean |

**Total issues detected: 5**

---

## Issues Found

- [MISSING] sorties.actual_start: 4 missing values
- [MISSING] sorties.actual_end: 4 missing values
- [MISSING] sorties.cancel_reason: 8 missing values
- [FLAG] Aircraft A002 (VT-SKY): high defect count = 8
- [FLAG] Aircraft A003 (VT-AIR): high defect count = 10

---

## Key Observations

### 1. Delay Mismatch in Sorties
- S001: Recorded delay = 20 min. Calculated from timestamps = 20 min. ✅ Match.
- S005: Recorded delay = 40 min. Calculated = 40 min. ✅ Match.
- All completed sorties' delay_minutes have been cross-validated against actual_start vs scheduled_start.

### 2. Payment Integrity
- All three cadets: `invoiced_amount - paid_amount = outstanding_amount` ✅ No discrepancy.
- C001: ₹2,50,000 − ₹2,10,000 = ₹40,000 ✅
- C002: ₹4,20,000 − ₹3,10,000 = ₹1,10,000 ✅
- C003: ₹1,80,000 − ₹90,000 = ₹90,000 ✅

### 3. Aircraft Defect Flags
- A002 (VT-SKY): 8 defects — elevated, contributed to cancellations
- A003 (VT-AIR): 10 defects — high concern, caused 2 cancellations at B02
- A001 (VT-ABC): 3 defects — acceptable level

### 4. Cancelled Sorties
- All 4 cancelled sorties correctly have no actual_start/actual_end ✅
- Cancel reasons are present for all cancelled sorties ✅

### 5. TOGA Study Coverage Gap
- C003 has only Navigation study records — no Meteorology or Air Regulations
- C002 has no Navigation records despite CPL requirement

### 6. Missing Values (Expected)
- sorties: actual_start, actual_end, cancel_reason — correctly null for cancelled sorties
- These are not errors; they are structurally correct nulls

---

## Recommendations

1. Add a `flight_hours_logged` column to sorties so total_flown_hours can be auto-calculated and cross-validated with cadets.csv
2. Enforce referential integrity — all cadet_ids in sorties should exist in cadets.csv
3. Add a `defect_threshold` alert system in Skynet for aircraft with defect_count > 5
4. TOGA should flag cadets who have not studied a subject required for their course
5. Consider adding GPS/ATC timestamps as a secondary source to validate delay_minutes
