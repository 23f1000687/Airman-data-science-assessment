# Finance & Operational Risk Analysis
**AIRMAN Aeronautics — Skynet Finance Module**
Generated: 2026-05-15

---

## Revenue Overview

| Metric | Amount |
|--------|--------|
| Total Invoiced | ₹850,000 |
| Total Collected | ₹610,000 |
| Total Outstanding | ₹240,000 |
| Collection Rate | 71.8% |

---

## Cadet Payment Risk Table

| Cadet | Outstanding | Payment % | Days Since Last Payment | Risk Score | Risk Level | Reason |
|-------|------------|-----------|------------------------|------------|------------|--------|
| Arjun Menon | ₹40,000 | 84.0% | 10d | 21.0 | Low | Moderate outstanding, recent payment |
| Meera Iyer | ₹1,10,000 | 73.8% | 25d | 48.1 | Medium | High outstanding + 25d gap |
| Rahul Nair | ₹90,000 | 50.0% | 35d | 73.0 | High | 50% unpaid + 35d payment gap |

---

## Key Finance Insights

### C001 — Arjun Menon — Low-Medium Risk
- ₹40,000 outstanding (16% of invoice). Last paid May 5 — 10 days ago. 
- Payment pattern is acceptable. No immediate training disruption expected.
- Recommendation: Send gentle reminder if no payment by May 25.

### C002 — Meera Iyer — High Risk
- ₹1,10,000 outstanding — **26.2% of total invoice unpaid**.
- Last payment: April 20 — **25 days ago**. No payment in nearly a month.
- This is a CPL student with 200h requirement — total course fee is ₹4,20,000. 
- Outstanding combined with slow training progress creates **dual risk**: financial default AND training dropout.
- **Recommendation**: Finance team to contact immediately. Payment plan or training hold may be required.

### C003 — Rahul Nair — High Risk
- ₹90,000 outstanding — **50% of total invoice unpaid**.
- Last payment: April 10 — **35 days ago**. Longest gap.
- Only ₹90,000 collected of ₹1,80,000 invoiced.
- Training already disrupted by aircraft defects — financial pressure adds further demotivation risk.
- **Recommendation**: Urgent finance + counseling intervention. Evaluate scholarship or EMI option.

---

## Revenue Leakage Indicators

1. **₹240,000 total outstanding** — 28.2% of total revenue at risk
2. C002 and C003 combined account for ₹2,00,000 outstanding — 82.6% of total AR
3. Average days since last payment: 23 days — above healthy 15-day threshold
4. No payment received from any cadet in the last 10 days (C001 was the most recent at 10 days)

---

## Training Continuity Risk

| Cadet | Risk | Impact on Training |
|-------|------|--------------------|
| C001 | Low | No immediate impact |
| C002 | High | May face training hold if ₹1,10,000 not cleared within 30 days |
| C003 | High | 50% unpaid — FTO may be unable to continue aircraft bookings |

---

## Recommendations for Finance Team

1. Implement payment milestone gates in Skynet: training slots auto-hold when outstanding > 25% of invoice
2. Automated WhatsApp/email reminders at 15d, 25d, 35d after last payment
3. Add payment status to CFI dashboard — training decisions need financial context
4. Explore EMI structuring for C003 (PPL is shorter course — smaller milestone payments may improve collection)
