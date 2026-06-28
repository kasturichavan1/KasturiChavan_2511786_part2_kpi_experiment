# Part 2: KPI Framework, Business Experiment Analysis & Decision Recommendation

## Repository Structure

```
part2_kpi_experiment/
├── data/
│   └── campaign_experiment_data.xlsx     # Source dataset (1,408 users)
├── analysis/
│   ├── experiment_analysis.xlsx          # Data quality checks, overall summary, segment analysis, hypothesis test
│   └── hypothesis_test_notes.md          # Full hypothesis test documentation
├── outputs/
│   ├── kpi_tree.png                      # Visual KPI tree diagram
│   ├── experiment_summary.xlsx           # Clean Control vs Treatment comparison + segment breakdown
│   └── recommendation_memo.md           # Executive recommendation memo
├── screenshots/
│   ├── summary_metrics.png              # Control vs Treatment metrics table
│   ├── hypothesis_test_output.png       # Z-test visualization and bar chart
│   └── kpi_tree_preview.png             # KPI tree preview image
└── README.md
```

---

## Business Context

A subscription-based digital product company launched a new onboarding and activation campaign. Users were randomly split into two groups:
- **Control (n=690):** Existing onboarding experience
- **Treatment (n=710):** New campaign experience

Leadership must decide whether to roll out the new campaign to all users. This analysis frames the business problem, defines success metrics, analyzes experiment results, evaluates guardrail metrics, and delivers a data-backed recommendation.

---

## Dataset Description

**File:** `data/campaign_experiment_data.xlsx`  
**Source sheet:** `experiment_data`  
**Original rows:** 1,408 | **After deduplication:** 1,400 (8 duplicate user_ids removed)

| Column | Type | Description |
|---|---|---|
| user_id | String | Unique user identifier |
| signup_date | Date | User signup date |
| experiment_group | String | Control or Treatment |
| region | String | North / South / East / West |
| device_type | String | Mobile / Desktop / Tablet (18 nulls) |
| traffic_source | String | Organic / Paid Search / Social / Referral / Email (24 nulls) |
| plan_type | String | Free / Basic / Premium |
| visited_landing_page | Binary (0/1) | Whether user visited landing page |
| started_trial | Binary (0/1) | Whether user started a trial |
| completed_onboarding | Binary (0/1) | Whether user completed onboarding |
| converted_to_paid | Binary (0/1) | Whether user converted to paid (**North Star**) |
| revenue_30d | Float | Revenue generated in 30 days ($) |
| support_tickets_30d | Integer | Number of support tickets raised |
| refund_requested | Binary (0/1) | Whether user requested a refund |
| days_to_convert | Float | Days from signup to conversion (NULL for non-converters) |
| engagement_score | Float | Engagement score 0–100 (14 nulls) |

---

## North Star Metric

**Selected: Paid Conversion Rate**

The Paid Conversion Rate is the proportion of users who converted to a paid subscription. It was selected as the North Star because:
- It directly measures the campaign's core objective
- It ties immediately to revenue generation
- It captures the end-to-end funnel outcome (not just intermediate steps)
- All other funnel metrics (visit rate, trial rate, onboarding rate) are drivers *of* conversion

**Risk of blind optimization:** Maximizing conversion rate alone could attract users who convert but generate low revenue or high support costs. This is exactly what the guardrail analysis revealed.

---

## KPI Tree Summary

The KPI tree (see `outputs/kpi_tree.png`) breaks the North Star into:

**Primary Driver 1: Acquisition & Reach**
- Landing Page Visit Rate → CTR, Bounce Rate
- Traffic Source Mix
- Device & Region Reach

**Primary Driver 2: Activation & Onboarding**
- Trial Start Rate → CTA Click Rate, Form Completion
- Onboarding Completion Rate → Step Drop-Off Rate, In-App Guide Usage
- Time to Activate (Days to Convert)

**Primary Driver 3: Revenue & Retention**
- ARPU → Plan Type Mix, Upsell Rate
- Revenue per Converted User
- Engagement Score → Feature Adoption, Session Frequency

**Guardrail Metrics:**
1. Refund Rate
2. Support Ticket Rate
3. Days to Convert
4. Segment-Level Conversion Drop
5. Revenue per Converted User

---

## Experiment Analysis Approach

### Data Cleaning Steps (documented in `analysis/experiment_analysis.xlsx` → "Data Quality Checks" sheet)

| Check | Finding | Action |
|---|---|---|
| Duplicate user_ids | 8 duplicates found | Removed; kept first occurrence |
| Missing device_type | 18 null values (1.3%) | Retained rows; excluded from device-level segment analysis |
| Missing traffic_source | 24 null values (1.7%) | Retained rows; excluded from traffic segment analysis |
| Missing days_to_convert | 1,336 nulls | Expected — nulls are correct for non-converters |
| Missing engagement_score | 14 nulls | Excluded from mean calculation only |
| Binary value integrity | All binary columns contain only 0 or 1 | No action needed |
| Revenue outliers | 15 values above 99th percentile (>$1,481) | Retained — premium users are valid |
| Group balance | Control=690, Treatment=710 after dedup | Acceptable 1.4% imbalance |
| Segment distribution | Region, device, plan type balanced across groups | No action needed |

### Metrics Calculated
All metrics listed in the assignment requirements were calculated in `outputs/experiment_summary.xlsx`, covering:
- Overall Control vs Treatment comparison (11 metrics)
- Segment breakdowns by region, device type, traffic source, and plan type

---

## Hypothesis Test Summary

**Test:** Two-Proportion Z-Test (One-Tailed)  
**Metric:** Paid Conversion Rate (North Star)  
**H0:** Conversion(Treatment) ≤ Conversion(Control)  
**H1:** Conversion(Treatment) > Conversion(Control)  
**Significance Level:** α = 0.05

| | Control | Treatment |
|---|---|---|
| Users | 690 | 710 |
| Conversions | 22 | 50 |
| Conversion Rate | 3.19% | 7.04% |

**Pooled proportion:** 0.05143  
**Standard Error:** 0.011749  
**Z-Statistic:** 3.264  
**P-Value (one-tailed):** 0.000549  
**Decision:** REJECT H0 — Result is statistically significant at the 5% level

See `analysis/hypothesis_test_notes.md` for full calculations and interpretation.

---

## Guardrail Metrics Considered

| Guardrail | Control | Treatment | Status |
|---|---|---|---|
| Revenue per Converted User | $1,630 | $770 | HIGH RISK — 52.8% drop, significant |
| Support Ticket Rate | 0.220 | 0.373 | HIGH RISK — 69% increase, significant |
| Refund Rate | 0.00% | 0.42% | LOW RISK — small absolute value, not significant |
| Days to Convert | 8.9 days | 6.4 days | POSITIVE — faster conversion |
| Segment-Level Conversion | Positive across all segments | Positive across all segments | POSITIVE — no segment declines |

---

## Final Recommendation

**CONDITIONAL LAUNCH — Phase in Treatment with active monitoring**

- **Phase 1:** Launch to Free plan users on Mobile and Tablet (highest lift, lowest risk)
- **Phase 2:** Expand to all users after 30-day review of guardrail metrics
- **Hold:** Do not launch to Premium users until revenue quality is investigated

The conversion rate improvement is statistically significant and commercially meaningful. However, the drop in revenue per converted user and the spike in support ticket rate require resolution before full-scale rollout.

See `outputs/recommendation_memo.md` for the complete executive memo.

---

## Assumptions and Limitations

1. Users were randomly assigned — no selection bias assumed
2. 30-day revenue window used; long-term LTV and churn are unknown
3. 8 duplicate user IDs removed (root cause unknown)
4. 18 device_type and 24 traffic_source nulls were excluded from segment-level analysis only
5. Revenue outliers (top 1%) were retained as legitimate premium users
6. Statistical tests assume independence between users

---

## Screenshots

| File | Description |
|---|---|
| `screenshots/summary_metrics.png` | Full Control vs Treatment metric comparison table |
| `screenshots/hypothesis_test_output.png` | Z-distribution visualization with rejection region and bar chart |
| `screenshots/kpi_tree_preview.png` | KPI tree diagram |
