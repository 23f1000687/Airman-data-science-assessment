# Executive Insight Report
**AIRMAN Aeronautics — Skynet + TOGA**
**Prepared for: FTO Leadership, CFI, Finance Team, Product Team**
Generated: 2026-05-15

---

## 1. Top 5 Operational Insights (Skynet)

### 1. Aircraft Defect Crisis at Base B02
A003 (VT-AIR, DA40) has 10 defects and 40% maintenance downtime. It is the **only aircraft at B02**, and it has caused 2 out of 3 scheduled sorties to be cancelled. Cadet C003 (Rahul Nair) is being grounded by infrastructure failure, not personal ability. **Immediate engineering inspection is required.**

### 2. One-Third of All Sorties Are Cancelled
Of 12 scheduled sorties, 4 were cancelled (33.3%). Split equally between Weather (2) and Aircraft Defect (2). Industry best practice for a well-managed FTO is under 10%. This indicates both external risk (weather) and internal risk (aircraft reliability) need systematic management.

### 3. Capt Menon Is Approaching Overload
At 160 duty hours and 96 flight hours (60% ratio), Capt Menon is the most utilized instructor. As the only instructor for Meera Iyer's CPL (200h requirement), this is a long-term sustainability concern. A CPL student needs consistent instructor continuity — any disruption to Capt Menon cascades directly to C002's training timeline.

### 4. Average 18-Minute Departure Delay Across All Completed Sorties
Seven of eight completed sorties had delays. Average delay is 18.1 minutes. Navigation sorties average 28+ minutes of delay. These delays compound into real training hours lost over a month. Dispatch readiness checklists and pre-flight notification systems would significantly reduce this.

### 5. A001 (VT-ABC, C172) Is the Most Reliable Asset
With only 3 defects and 13% downtime, VT-ABC has the best availability and zero defect cancellations. Scheduling priority should be given to this aircraft, particularly for cadets with critical milestone lessons approaching.

---

## 2. Top 5 Training Progress Insights

### 1. C003 Is at Risk for the Wrong Reasons
Rahul Nair has the lowest flight progress (26.7%), but 66.7% of his sorties were cancelled due to aircraft defect — not due to cadet-side issues. Treating this as a cadet performance problem would be a misdiagnosis. **Fix the aircraft; the cadet will catch up.**

### 2. C002 Is Behind on a 200-Hour Course
Meera Iyer is only 37% through her CPL with an estimated 303 more days needed at her current flying rate. A CPL is a long, demanding course. The FTO should treat her training continuity as a strategic risk — losing a CPL student to dropout is a significant revenue and reputational loss.

### 3. C001 Is the Benchmark Cadet This Cohort
Arjun Menon has 63.3% flight progress, zero cancellations, and active TOGA engagement. He is the only cadet on track for timely completion. His patterns — consistent scheduling, no delays due to cadet-side factors — should inform best practices for the other cadets.

### 4. Weather Is Systematically Affecting B01 Navigation Sorties
Both weather cancellations affected B01 cadets flying Navigation. Scheduling Navigation sorties for early morning or checking METAR forecasts the evening before could reduce this significantly.

### 5. Cadet Flying Rates Are Unsustainably Low
C003: 0.143h/day. C002: 0.416h/day. C001: 0.228h/day. Even the best-performing cadet is averaging under 15 minutes of flight time daily. FTOs typically target 1–2h/day for active training. Increased sortie frequency is the highest-leverage intervention available.

---

## 3. Top 3 TOGA Personalization Opportunities

### 1. Inactivity-Triggered Study Recommendations
C003 has been inactive for 17 days. TOGA should auto-send a push notification with a specific study prompt: "You have a Navigation sortie coming up — review Chapter 3: VOR Navigation." Rather than generic reminders, content should be tied to upcoming lessons.

### 2. Course-Specific Content Depth
C002 (CPL) needs deeper Air Regulations and Meteorology content than PPL cadets. TOGA currently does not appear to differentiate content depth by course level. A CPL learner studying the same Air Regulations content as a PPL student will underperform in written exams.

### 3. Post-Flight Study Pairing
After each completed sortie, TOGA should suggest study content aligned to the lesson just flown. A cadet who just completed a Navigation sortie should see "Review: Reading Aeronautical Charts" — creating a flight-study feedback loop that reinforces learning.

---

## 4. Top 3 Finance Risks

### 1. ₹2,40,000 Total Outstanding — 28.2% of All Revenue at Risk
Across three cadets, ₹2,40,000 is outstanding. C002 and C003 together account for ₹2,00,000. At current collection rate (71.8%), the FTO risks revenue leakage that can affect aircraft maintenance budgeting and instructor salary sustainability.

### 2. C003 is 50% Unpaid with a 35-Day Payment Gap
Rahul Nair has paid only ₹90,000 of ₹1,80,000 invoiced. The last payment was 35 days ago. Combined with the B02 aircraft problems, this cadet is at the highest risk of dropout. A proactive payment plan — tied to training milestones — could improve retention and cash flow.

### 3. C002's CPL Will Cost ₹4,20,000+ — Outstanding Must Be Resolved Before Midpoint
CPL training courses typically have multiple invoice milestones. With ₹1,10,000 already outstanding after only 37% completion, C002's financial trajectory suggests the total outstanding could grow significantly without intervention. A payment plan or training hold decision must be made within 30 days.

---

## 5. Product Recommendations for Skynet

1. **Maintenance Alert Module**: Flag any aircraft with defect_count > 5 with a "Review Required" status in the scheduling dashboard. Auto-block the aircraft from new sortie assignments until cleared.

2. **Dispatch Readiness Score**: Before each sortie, Skynet computes a real-time score (aircraft availability + weather forecast + instructor readiness + cadet payment status). A score below threshold triggers a 24h advance warning.

3. **CFI Dashboard with Risk Overlays**: A single-screen view showing all cadets' flight progress, TOGA study engagement, payment status, and risk score — so the CFI can make daily decisions with full context.

4. **Weather Contingency Protocol**: When a sortie is cancelled due to weather, Skynet automatically offers to log a "Ground Briefing" session and suggests a replacement activity (simulator, study, pre-flight planning).

5. **Instructor Load Monitor**: Real-time tracking of each instructor's monthly flight hours vs DGCA FIR regulatory limits. Alert when within 20% of the cap.

---

## 6. Product Recommendations for TOGA

1. **Study Readiness Score on Dashboard**: Show cadets their overall readiness score (as computed in this analysis) — but frame it positively as "Your Exam Readiness: 59%". Include a breakdown by subject.

2. **Pre-Flight Briefing Module**: 30 minutes before a scheduled sortie, TOGA pushes a targeted "Pre-Flight Study" prompt relevant to that day's lesson type. This bridges theoretical and practical training.

3. **Adaptive Quiz Difficulty**: For subjects where a cadet scores below 60%, TOGA should serve easier foundational questions first, then ramp up difficulty. Current flat quiz difficulty may discourage low-scoring cadets.

4. **Instructor-Visible Study Insights**: Allow CFI to see each cadet's last 7-day study activity, weak subjects, and quiz scores from within Skynet. Study performance should inform flight scheduling decisions.

5. **Streak and Engagement Gamification**: Simple engagement mechanics (study streaks, milestone badges for completing a chapter set) increase daily active use — critical for cadets like C003 who are disengaging.

---

## 7. Data Quality Issues Found

1. **Missing actual_start/actual_end for cancelled sorties** — structurally correct nulls, but pipeline should explicitly validate this rule
2. **Aircraft A002 and A003 have high defect counts** (8 and 10) that meet flagging thresholds — no automated alert triggered in current data
3. **TOGA data is incomplete for all cadets** — C002 has no Navigation records; C003 has no Meteorology or Air Regulations records
4. **No automatic cross-validation between sorties.delay_minutes and timestamp difference** — delays can be misreported without detection
5. **Payments: no payment milestone structure** — only total invoice and total paid; intermediate milestones not tracked

---

## 8. Suggested Next Data Fields AIRMAN Should Collect

| Dataset | New Field | Reason |
|---------|-----------|--------|
| sorties.csv | `flight_hours_logged` | Auto-compute and cross-validate cadet total_flown_hours |
| sorties.csv | `weather_condition_at_dispatch` | Link weather data to cancellation decisions analytically |
| sorties.csv | `cadet_readiness_score` (pre-sortie) | Track cadet preparation before each flight |
| cadets.csv | `target_completion_date` | Enable deadline-based risk scoring |
| toga_study.csv | `session_duration_minutes` | Measure study effort, not just chapter count |
| toga_study.csv | `last_quiz_attempt_date` | Separate quiz recency from study recency |
| payments.csv | `payment_milestone` | Track which training phase has been paid for |
| aircraft.csv | `last_inspection_date` | Correlate defect count with maintenance recency |
| instructors.csv | `available_hours_this_month` | Real-time load management |

---

## 9. Final Recommendation to AIRMAN Leadership

**The data tells one clear story: this is a small cohort under significant multi-dimensional stress.**

The three cadets represent three different risk profiles:
- **C001**: On track. Protect this cadet's schedule and maintain study momentum.
- **C002**: Dual financial and training risk. A CPL dropout is expensive — intervene now, not after the next invoice.
- **C003**: Infrastructure victim. Fix the B02 aircraft. Then watch C003's progress recover.

The data also shows that Skynet and TOGA, when integrated, can create a genuinely intelligent training management system. The insight layer this analysis demonstrates — connecting flight operations, study behavior, and financial health into a single risk score — is exactly what FTO leadership needs but cannot manually compute across dozens of cadets.

**The immediate priorities for AIRMAN:**
1. Resolve A003 (B02) aircraft reliability — operational blocker
2. Finance intervention for C002 and C003 — revenue protection
3. Build the CFI risk dashboard in Skynet — product impact
4. Enable TOGA inactivity alerts — low-effort, high-retention impact
5. Collect richer data (weather, session duration, milestones) to power the next intelligence layer

AIRMAN has the right product vision. The data infrastructure just needs to catch up.
