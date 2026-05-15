# Methodology Document
**AIRMAN Aeronautics — Cadet Risk Score & Analytical Methodology**
Generated: 2026-05-15

---

## Risk Score Formula

### Design Philosophy

The goal was a **transparent, auditable formula** — not a black-box ML model. Aviation training involves real people's careers and safety. Any score that affects scheduling or intervention decisions must be explainable to the cadet, CFI, and FTO management.

### Formula

```
Risk Score = Σ (Component Score × Weight)

Components:
  Flight Progress Risk    = (1 - flight_progress_pct / 100)           × 25 pts
  Study Progress Risk     = (1 - avg_chapter_progress / 100)           × 15 pts
  Quiz Score Risk         = (1 - avg_quiz_score / 80)                  × 15 pts
  Study Inactivity Risk   = min(days_inactive / 30, 1)                 × 10 pts
  Payment Risk            = outstanding_pct / 100                      × 20 pts
  Cancellation Rate Risk  = cancel_rate / 80                           × 10 pts
  Average Delay Risk      = min(avg_delay_min / 60, 1)                 ×  5 pts
                                                                    ─────────
                                                    Total Max =       100 pts
```

All components are clipped to [0, 1] before multiplying by their weight.

### Risk Levels
```
 0–39 = Low    (green)
40–69 = Medium (amber)
70–100 = High  (red)
```

---

## Feature Justification

| Feature | Weight | Justification |
|---------|--------|---------------|
| Flight Progress | 25 | The primary KPI of training — directly determines course completion |
| Payment Outstanding | 20 | Training continuity is legally and practically contingent on fees |
| Study Progress | 15 | Ground knowledge is a prerequisite for flight tests; DGCA requires written exam pass |
| Quiz Score | 15 | Quiz performance predicts written examination outcome |
| Cancellation Rate | 10 | High cancellation rate disrupts training continuity and momentum |
| Study Inactivity | 10 | Extended gaps predict disengagement and dropout risk |
| Average Delay | 5 | Chronic delay is a weak but real signal of scheduling/readiness issues |

**Payment is weighted second-highest (20)** because financial default directly stops training — an FTO cannot continue providing flights if fees are not collected.

**Quiz score is weighted separately from study progress (15 each)** because chapter completion and comprehension are different signals. A cadet can complete chapters without retaining knowledge.

---

## Computed Risk Scores

| Cadet | Score | Level | Main Reasons |
|-------|-------|-------|--------------|
| C001 — Arjun Menon | 22.5 | Low | Some outstanding payment, moderate study scores |
| C002 — Meera Iyer | 45.9 | Medium | Low CPL progress, weak quiz scores, payment risk |
| C003 — Rahul Nair | 62.8 | Medium | Lowest flight progress, longest inactivity, highest payment risk |

---

## Explainability Questions

### 1. Why did you choose your risk score formula?

I chose a **weighted linear additive model** because it is fully interpretable. Every point in the score can be traced to a specific data field with a clear real-world meaning. The weights reflect relative business impact — flight progress is the primary objective of an FTO, so it gets the highest weight. A random forest or neural network would perform similarly on 3 data points but would produce a number that no CFI could explain or challenge.

The formula is deliberately simple. With a small dataset (3 cadets), any ML model would be overfitting. A formula also has the advantage of being directly auditable — if a cadet scores 65, we can show them exactly which 3 factors contributed the most points.

### 2. Which features had the most impact and why?

**Flight progress (25 pts)** had the most theoretical impact — but in practice, all three cadets had low flight progress relative to course requirements, which compressed differentiation. **Payment outstanding (20 pts)** was the strongest differentiator: C001 had 16% outstanding, C002 had 26%, C003 had 50%. This single feature explains most of the spread between C001 (low risk) and C003 (highest risk).

**Cancellation rate** was informative but partly confounded — C003's 66.7% cancellation rate is driven by aircraft defect, not cadet behavior. This is the formula's most important limitation.

### 3. What assumptions did you make?

1. **Equal weights are starting points**: The weights assigned (25, 20, 15, etc.) are reasonable priors, not empirically calibrated. Real weights should be derived from historical data on which features predicted dropout or exam failure.

2. **All cadets are full-time trainees**: The flying rate calculation assumes cadets train every day. Part-time or self-funded cadets may have naturally lower rates without higher risk.

3. **Quiz scores are comparable across subjects**: Meteorology and Navigation quizzes may have different difficulty levels. A 62% in Meteorology may not be equivalent to a 62% in Navigation.

4. **Cancellation causes are not separated**: Weather cancellations and aircraft defect cancellations both count against the cadet's "cancellation rate" — but only aircraft defect cancellations are operationally addressable. The formula currently penalizes C003 for infrastructure failure.

5. **Reference date is 2026-05-15**: All "days inactive" and "days since payment" calculations are relative to this date.

### 4. What data quality issue could mislead the model?

The most dangerous issue is **causation conflation in cancellation rate**. C003 has a 66.7% cancellation rate, but all cancellations were due to Aircraft Defect — a factor completely outside the cadet's control. If the model's score is used to rank cadets for resources or attention, C003 would appear riskier than warranted on this dimension.

A secondary issue: **flown hours are taken from cadets.csv as a static field**, not computed from sorties.csv. These two could diverge if sorties are logged outside the system. The sorties data shows approximately 12h of flight activity (computed from actual_start/actual_end), but cadets.csv states 28.5h, 74h, and 12h — the gap for C001 and C002 suggests historical data not in this extract.

### 5. What would you not automate or predict yet?

1. **Training hold decisions**: The risk score should flag a case for human review, not automatically suspend a cadet's schedule. Training holds have legal, contractual, and psychological consequences.

2. **Exam readiness certification**: A quiz score in TOGA is not an official readiness indicator for DGCA written examinations. Automating "ready/not ready" based on TOGA data alone would be premature and potentially harmful.

3. **Instructor performance evaluation**: Instructor utilization ratios and flight/duty percentages are informative but insufficient to evaluate instructor quality. Context matters — Capt Sharma's low utilization is caused by B02 aircraft issues, not instructor performance.

4. **Financial default prediction**: Three data points with one payment observation per cadet is insufficient to build a reliable payment default model. More historical payment behavior is needed.

### 6. How would you validate this model with real FTO data?

1. **Historical validation**: Collect 12+ months of cadet data. For each cadet, compute the risk score at months 1, 3, 6. Then check whether high-risk scores at month 3 predicted dropout, exam failure, or training extension by month 12.

2. **Expert calibration**: Present the risk scores to experienced CFIs and ask them to rank cadets by their perceived risk. Measure rank correlation (Spearman's ρ) between model scores and CFI rankings. Adjust weights where disagreement is systematic.

3. **A/B intervention**: For medium-risk cadets, randomly assign intervention (CFI check-in, TOGA push) vs. no intervention. Track outcome. This measures the score's actionability, not just its accuracy.

4. **Calibration plot**: Plot risk score deciles vs actual dropout/delay rates. A well-calibrated model shows monotonically increasing dropout rates as the score increases.

### 7. How would you prevent unfair ranking of cadets?

1. **Decompose controllable vs non-controllable risk**: Separate cancellation rate into "cadet-caused" (e.g., no-show) and "external" (weather, aircraft defect). Only the former should affect a cadet's personal risk score.

2. **Disclose the score and its components to the cadet**: Cadets should be able to see their score and the specific factors contributing to it — this creates fairness through transparency.

3. **Never use the score as the sole decision variable**: The score is a triage tool to direct human attention, not a pass/fail gate.

4. **Avoid proxy discrimination**: If cadets at remote bases systematically get lower scores due to aircraft reliability issues (as C003 does), the score will unfairly penalize cadets based on geography — a factor unrelated to their ability or effort.

5. **Regular audits**: Quarterly review of score distributions across bases, courses, and enrollment cohorts. If any group is systematically scored higher without a substantive reason, recalibrate.

### 8. How should AIRMAN display this insight without demotivating students?

1. **Frame as "readiness" not "risk"**: Show cadets a "Study Readiness: 62%" rather than "Risk Score: 38%". The goal is encouragement, not judgment.

2. **Show the actionable fix alongside the score**: "Your Meteorology readiness is 42%. Completing 5 more chapters would raise this to 58%." The score alone without guidance is demoralizing.

3. **Show progress, not just current state**: "Your overall readiness improved 8 points since last week" is more motivating than an absolute score.

4. **Only show the full risk breakdown to the CFI/FTO team** — the cadet sees a friendly version; the instructor sees the complete analytical view.

5. **Avoid numeric scores for cadets entirely**: Consider showing only a colored status indicator (green/amber/red) with a qualitative message for cadet-facing dashboards.

### 9. What additional data would improve your model?

| Data | Impact |
|------|--------|
| Historical dropout/delay outcomes | Enables supervised learning — calibrate weights empirically |
| Weather conditions at dispatch | Separate weather-caused cancellations from avoidable ones |
| Simulator session hours | A cadet using simulator on weather-cancel days is not at risk |
| DGCA written exam scores | The ground truth for study readiness — better than quiz scores |
| Cadet self-reported confidence rating | Psychometric signal for risk beyond behavioral data |
| Payment plan structure | Understand if outstanding is on-plan vs overdue |
| Session duration in TOGA | Time spent studying, not just chapters clicked |
| Sortie pre-briefing completion | Did the cadet prepare for the lesson? |

### 10. How would this analysis help Skynet and TOGA become more intelligent products?

**Skynet becomes intelligent when it connects operational data to decisions**. Today, an FTO admin manually checks aircraft logs, instructor availability, and cadet progress in separate places. The analytics layer built here — aircraft utilization, dispatch reliability, instructor load — can become Skynet's live operations dashboard. Over time, with more data, Skynet can predict which days will have high cancellation risk (weather pattern + aircraft maintenance schedule) and suggest preemptive rescheduling.

**TOGA becomes intelligent when it personalizes learning pathways**. The study readiness score and weak-subject identification in this analysis is a prototype of TOGA's recommendation engine. Instead of a flat content library, TOGA can use each cadet's quiz history, inactivity patterns, and upcoming lesson type to serve exactly the right content at the right time. The flight-study correlation analysis (scatter plot) shows that study progress and flight progress are not always aligned — TOGA's job is to close that gap proactively.

Together, Skynet + TOGA become a **closed-loop training intelligence system**: flight data informs study recommendations; study performance informs flight scheduling readiness; payment data informs operational continuity. The risk score is the bridge between these layers.

---

## Limitations

1. Dataset is very small (3 cadets, 12 sorties) — all conclusions are directional, not statistically significant
2. Risk score weights are expert-assigned, not data-derived
3. No temporal trend analysis possible with a single week of sortie data
4. TOGA study data is sparse — multiple cadets have no records for required subjects
5. Aircraft utilization percentages appear low partly because this is a short time window extract, not full monthly data
6. No control group to measure intervention effectiveness

---

## Tools & Libraries Used

| Tool | Version | Purpose |
|------|---------|---------|
| Python | 3.11 | Core language |
| pandas | 2.x | Data manipulation |
| numpy | 1.x | Numerical computation |
| matplotlib | 3.x | Chart generation |
| seaborn | 0.x | Statistical visualization |
| Jupyter Notebook | Latest | Interactive analysis |
