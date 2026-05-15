# AIRMAN Aeronautics — Data Science Assessment
## Skynet + TOGA Intelligence | Data Scientist Intern

---

## Project Overview

This project delivers a complete data intelligence analysis for **AIRMAN Aeronautics** covering two core products:
- **Skynet**: Flight school and aviation academy operations SaaS
- **TOGA**: AI-powered pilot learning, logbook, and pre-flight planning app

The analysis converts simulated aviation training, operations, study, and finance data into actionable insights for the FTO operations team, Chief Flying Instructor (CFI), finance management, and TOGA product team.

---

## Folder Structure

```
airman-data-science-assessment/
├── data/
│   ├── sorties.csv              # Sortie/flight scheduling & actuals
│   ├── aircraft.csv             # Fleet data with utilization & defects
│   ├── cadets.csv               # Cadet enrollment and flight hours
│   ├── instructors.csv          # Instructor duty and flight hours
│   ├── toga_study.csv           # TOGA app study activity per cadet
│   ├── payments.csv             # Cadet payment and outstanding amounts
│   ├── risk_scores.csv          # Output: Computed cadet risk scores
│   └── cleaned_outputs.csv      # Output: Merged, cleaned dataset
├── notebooks/
│   └── analysis.ipynb           # Full analysis notebook (all 8 tasks)
├── reports/
│   ├── data_quality_report.md   # Task 1: Data validation findings
│   ├── skynet_operations_analysis.md  # Task 2: Ops analytics
│   ├── training_progress_analysis.md  # Task 3: Cadet training
│   ├── toga_study_intelligence.md     # Task 4: Study analytics
│   ├── finance_risk_analysis.md       # Task 5: Payment risk
│   ├── executive_insights.md          # Task 8: Leadership report
│   └── methodology.md                 # Task 6 explainability + Q&A
├── charts/
│   ├── aircraft_utilization.png
│   ├── cancellation_reasons.png
│   ├── cadet_progress.png
│   ├── study_readiness.png
│   ├── payment_risk.png
│   ├── cadet_risk_scores.png
│   └── flight_vs_study_progress.png
└── README.md
```

---

## Tools & Libraries

| Library | Purpose |
|---------|---------|
| `pandas` | Data loading, cleaning, transformation |
| `numpy` | Numerical computation |
| `matplotlib` | Chart generation (all 7 charts) |
| `seaborn` | Statistical chart styling |
| `datetime` | Date arithmetic for risk calculations |
| `Jupyter Notebook` | Interactive analysis environment |

No external APIs or paid tools were used. All analysis runs offline.

---

## Setup Instructions

### Prerequisites
- Python 3.8+
- pip

### Install Dependencies
```bash
pip install pandas numpy matplotlib seaborn jupyter
```

### Run the Notebook
```bash
cd airman-data-science-assessment
jupyter notebook notebooks/analysis.ipynb
```

Or run the full analysis as a script:
```bash
python notebooks/run_analysis.py
```

---

## Data Assumptions

1. **Reference date** is 2026-05-15 (today) for all "days since" calculations
2. **Cancelled sorties** correctly have null actual_start and actual_end — this is structurally valid, not a data error
3. **sorties.csv delay_minutes** was cross-validated against actual_start vs scheduled_start timestamps for all completed sorties
4. **total_flown_hours in cadets.csv** represents cumulative flight hours including data outside this sortie extract
5. **Aircraft utilization** is computed as actual flight hours from this period / total_available_hours — will appear low because only one week of sorties is in the extract
6. **Study readiness** components use a 80% quiz score ceiling (not 100%) because aviation exam pass thresholds are typically 70–75%, and 80% represents a comfortable buffer

---

## Metrics Calculated

### Skynet Operations
- Aircraft utilization % = actual_flown_hours / total_available_hours × 100
- Downtime % = maintenance_downtime_hours / total_available_hours × 100
- Instructor flight-to-duty ratio = total_flight_hours / total_duty_hours × 100
- Dispatch completion rate = completed sorties / total sorties × 100
- Cancellation rate by reason, base, lesson type

### Training Progress
- Flight progress % = total_flown_hours / total_required_hours × 100
- Flying rate (h/day) = total_flown_hours / days_enrolled
- Estimated days to completion = remaining_hours / flying_rate

### TOGA Study
- Chapter progress % = chapters_completed / total_chapters × 100
- Subject readiness = (chapter_pct × 0.4) + (quiz_score × 0.4) + (practice_factor × 0.2)
- Days inactive = REF_DATE − last_active_date

### Finance
- Payment completion % = paid_amount / invoiced_amount × 100
- Outstanding % = outstanding_amount / invoiced_amount × 100
- Days since last payment = REF_DATE − last_payment_date

---

## Risk Score Explanation

The cadet risk score (0–100) is a **transparent, weighted additive model** — no black-box ML.

```
Risk Score = 
    Flight Progress Risk  (25 pts)  +
    Payment Risk          (20 pts)  +
    Study Progress Risk   (15 pts)  +
    Quiz Score Risk       (15 pts)  +
    Cancellation Risk     (10 pts)  +
    Study Inactivity Risk (10 pts)  +
    Average Delay Risk    ( 5 pts)
```

Each component is normalized to 0–1, then multiplied by its weight. Higher score = higher risk.

| Score | Level |
|-------|-------|
| 0–39  | Low   |
| 40–69 | Medium |
| 70–100 | High |

**Why this formula?** Every component can be traced to a real business impact. Payment affects training continuity. Flight progress determines course completion. Quiz scores predict exam outcomes. The formula is auditable and can be challenged or adjusted by CFI or FTO management.

---

## Key Outputs

| Output | Location |
|--------|----------|
| Cadet risk scores | `data/risk_scores.csv` |
| All 7 charts | `charts/` |
| Executive report | `reports/executive_insights.md` |
| Methodology + Q&A | `reports/methodology.md` |

**Risk Score Summary:**
- C001 Arjun Menon: **22.5 — Low Risk** ✅
- C002 Meera Iyer: **45.9 — Medium Risk** ⚠️
- C003 Rahul Nair: **62.8 — Medium Risk** ⚠️ (driven by aircraft infrastructure, not cadet performance)

---

## Known Limitations

1. **Very small dataset** (3 cadets, 12 sorties, 1 week) — insights are directional, not statistically significant
2. **Risk score weights are expert-assigned**, not empirically calibrated from historical outcomes
3. **No temporal trend analysis** with a single week of data
4. **TOGA data is sparse** — cadets missing multiple mandatory subjects
5. **Utilization metrics appear low** because this is a short extract, not a full monthly dataset
6. **Cancellation rate conflates cadet-caused and infrastructure-caused cancellations** — C003 is penalized for B02 aircraft issues

---

## What I Would Improve With More Time

1. **Build a Jupyter Notebook with interactive widgets** (ipywidgets) so the CFI can adjust risk weights and see scores update live
2. **Add time series plots** to show training velocity trends week-over-week
3. **Separate controllable vs external cancellation reasons** in the risk formula
4. **Connect to live DGCA weather METAR API** to predict next-week cancellation risk by base
5. **Build a Streamlit dashboard** as a prototype Skynet operations screen
6. **Add confidence intervals** to the estimated completion dates (assuming flying rate has variance)
7. **Interview a CFI** to calibrate the risk weights against expert judgment before production use

---

## AI Usage Disclosure

### 1. Did you use AI tools? If yes, where?
Yes. Claude (Anthropic) was used as a coding and writing assistant throughout this assessment.

### 2. What prompts or tasks did AI help with?
- Structuring the analysis pipeline and folder layout
- Writing Python code for data loading, validation, and chart generation
- Drafting the markdown reports (data quality, operations, training, TOGA, finance, executive)
- Drafting the methodology Q&A responses

### 3. Which parts did you personally verify?
- All computed metrics were manually cross-checked (e.g., 250,000 − 210,000 = 40,000 ✅)
- Risk score formula logic was traced through manually for each cadet
- Chart outputs were visually reviewed and corrected where needed
- All aviation domain interpretations were verified against my understanding of FTO operations (DGCA regulations, PPL/CPL hour requirements, instructor duty limits)

### 4. Which AI suggestion did you reject or modify?
- Initial risk weights had quiz score at 20 and payment at 15 — I adjusted to 15 and 20 respectively because payment directly halts training, which is a harder constraint than quiz performance
- AI initially proposed using sklearn for a logistic regression model — I rejected this as unnecessarily complex for 3 data points and replaced with the explicit formula

### 5. Which part of the analysis are you least confident about?
The risk score weights. These are reasonable priors, but without historical outcome data (who actually dropped out, who failed exams), I cannot know if the weights are correctly calibrated. The formula structure is sound; the weights need empirical validation.

### 6. Explain one formula in your own words
**Flying Rate (h/day)**: Take the total hours a cadet has flown (from cadets.csv). Divide by the number of days since they enrolled (calculated as today's date minus enrollment_date). This gives us how many flight hours they complete per day on average. Then, to estimate how long until they finish the course, divide the remaining hours by this rate. For C002 Meera Iyer: 126 remaining hours ÷ 0.416 h/day = ~303 more days. That's the projected timeline — and it tells us she needs to fly much more frequently to complete CPL on time.

---

*Assessment completed for AIRMAN Aeronautics Data Scientist Intern role.*
*Contact: Kaushik Gaur | 23f1000687@ds.study.iitm.ac.in*
