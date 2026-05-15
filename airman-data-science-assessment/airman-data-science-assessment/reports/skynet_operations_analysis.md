# Skynet Operations Analytics Report
**AIRMAN Aeronautics — Flight Training Organisation**
Generated: 2026-05-15

---

## 1. Aircraft Utilization

| Aircraft | Registration | Type | Available Hrs | Downtime Hrs | Flown Hrs | Utilization % | Defects |
|----------|-------------|------|--------------|-------------|-----------|--------------|---------|
| A001 | VT-ABC | C172 | 180 | 24 | 7.5 | 4.2% | 3 |
| A002 | VT-SKY | PA28 | 160 | 48 | 3.0 | 1.9% | 8 ⚠️ |
| A003 | VT-AIR | DA40 | 150 | 60 | 1.5 | 1.0% | 10 🔴 |

**Key Findings:**
- All three aircraft are significantly underutilized (all under 5% of available hours in this period).
- This is a data window issue — only 12 sorties are captured. The utilization metric will improve with full monthly data.
- A002 (VT-SKY, PA28) has **8 defects** and 30% downtime — directly causing 1 cancellation (S002 mechanism via I002).
- A003 (VT-AIR, DA40) has **10 defects** and 40% downtime — caused 2 cancellations at B02. **Immediate operational review recommended.**
- A001 (VT-ABC, C172) has the best reliability with only 3 defects and 13% downtime.

### Underutilized Aircraft
All aircraft have net operational hours well above actual usage. No aircraft is being used at full capacity. Root cause: small cadet cohort (3 cadets), cancellations reducing effective utilization.

### Aircraft Requiring Operational Review
- **A003 (VT-AIR)**: 10 defects, 60h downtime of 150 available. Recommend engineering inspection and defect root cause analysis.
- **A002 (VT-SKY)**: 8 defects, 48h downtime. Recommend pre-flight defect checks to be escalated.

---

## 2. Base-wise Utilization

| Base | Total Available Hrs | Total Flown Hrs | Total Downtime Hrs | Base Utilization % |
|------|--------------------|-----------------|--------------------|-------------------|
| B01 | 340 | 10.5 | 72 | 3.1% |
| B02 | 150 | 1.5 | 60 | 1.0% |

- B01 has two aircraft and two instructors. Higher throughput but PA28 (A002) is a reliability risk.
- B02 has a single aircraft (DA40/A003) which is the most defect-prone. Only 1 sortie completed vs 3 planned.

---

## 3. Instructor Utilization

| Instructor | Base | Duty Hours | Flight Hours | Flight/Duty Ratio | Sorties Done |
|------------|------|------------|-------------|-------------------|-------------|
| Capt Rao | B01 | 145 | 82 | 56.6% | 5 |
| Capt Menon | B01 | 160 | 96 | 60.0% | 2 |
| Capt Sharma | B02 | 110 | 52 | 47.3% | 1 |

**Key Findings:**
- Capt Menon has the highest duty hours (160h) and flight hours (96h) — approaching a potential overload.
- Capt Sharma's flight/duty ratio is lowest (47.3%) — either underutilized or has more ground duties. B02 aircraft unreliability is a likely cause.
- No qualification mismatches detected: I001↔C172, I002↔PA28, I003↔DA40 — all matched.
- **Recommendation**: Monitor Capt Menon's hours as cadet C002 (CPL) has 200 hours total requirement — significant future load.

---

## 4. Dispatch Reliability

| Metric | Value |
|--------|-------|
| Total Sorties Scheduled | 12 |
| Completed | 8 (66.7%) |
| Cancelled | 4 (33.3%) |
| Completed with Delay | 7 |
| Average Delay (completed sorties) | 18.1 minutes |

### Cancellation Breakdown
| Reason | Count | % of Cancellations |
|--------|-------|-------------------|
| Weather | 2 | 50% |
| Aircraft Defect | 2 | 50% |

### Insights
- 33.3% cancellation rate is high. Industry best practice targets <10% for well-managed FTOs.
- Weather cancellations (50%) are external and unavoidable, but scheduling mitigation (early AM slots, alternate lesson plan) can help.
- Aircraft Defect cancellations (50%) are **operationally addressable** — better pre-flight maintenance scheduling would reduce these.
- Average delay of 18.1 minutes across completed sorties is significant — most delays are departure delays (late instructor/cadet readiness).
- Navigation lessons see higher delays (avg ~30 min) vs Circuit sorties (avg ~8 min) — may indicate more complex preflight planning requirements.

---

## 5. Actionable Skynet Recommendations

1. **Maintenance alert system**: Auto-flag aircraft with defect_count > 5 for review before next sortie scheduling.
2. **Delay dashboard**: Show CFI a live delay trend by lesson type and instructor so patterns are caught early.
3. **Weather contingency module**: When weather cancellation is logged, auto-suggest a ground briefing or simulator session as substitute.
4. **Instructor load monitoring**: Alert when any instructor's monthly flight hours approach regulatory maximum (DGCA FIR limits).
5. **B02 risk flag**: Skynet should auto-generate an operational risk alert when a single-aircraft base has 2+ defect cancellations in a week.
