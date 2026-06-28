# Recommendation Memo
## Onboarding & Activation Campaign — Experiment Decision

**To:** Leadership / Product & Growth Teams  
**From:** Business Analyst  
**Date:** June 2025  
**Subject:** A/B Experiment Results — Launch Recommendation for New Onboarding Campaign  
**Decision Required:** Launch, Do Not Launch, Segment-Only Launch, or Continue Testing

---

## 1. Executive Summary

The new onboarding and activation campaign (Treatment) significantly outperformed the existing experience (Control) on the North Star metric — **Paid Conversion Rate increased by +120.8%** (from 3.19% to 7.04%), a result that is statistically significant (Z=3.264, p=0.0005).

Engagement scores also improved substantially (+10.4%), and users converted 2.5 days faster.

However, two guardrail metrics raise concern: **support ticket rate increased by 69%**, and **revenue per converted user dropped by 52.8%** in the Treatment group ($770 vs $1,630 in Control). These signals suggest the campaign may be attracting lower-value users or creating friction post-conversion.

**Recommendation: Conditional Launch — Phase in Treatment for Free plan users and Mobile/Desktop users while investigating the revenue quality and support ticket signals before full rollout.**

---

## 2. North Star Metric

**Selected North Star: Paid Conversion Rate**

The Paid Conversion Rate is the single most important outcome metric for this experiment because:
- It directly measures the campaign's core objective: converting users to paying subscribers
- It ties directly to revenue generation and business growth
- It is a clear, unambiguous binary signal (converted = 1, not converted = 0)
- It captures the full funnel effect from onboarding through to purchasing intent

**Why not other metrics?**
- *Landing Page Visit Rate* — too early in funnel; does not confirm revenue intent
- *Trial Start Rate* — conversion to trial does not guarantee paid conversion
- *Engagement Score* — engagement is a leading indicator, not a revenue outcome
- *ARPU* — ARPU was not significantly different between groups (p=0.91)

**Risk of blind optimization:** Optimizing purely for conversion rate could attract lower-intent users who convert initially but churn, request refunds, or generate high support costs — exactly what some guardrail signals hint at.

---

## 3. KPI Tree Summary

The KPI tree structures the North Star into three primary driver areas:

**Acquisition & Reach** (Landing page visit rate → traffic source mix → device/region reach)  
These metrics measure whether users are even reaching the campaign entry point. Treatment showed a significant +8.73pp lift in landing page visits, indicating strong top-of-funnel improvement.

**Activation & Onboarding** (Trial start rate → onboarding completion rate → days to activate)  
Treatment improved onboarding completion by +5.49pp (significant) and reduced days to convert by 2.5 days. Users in Treatment are engaging more deeply and faster with the product.

**Revenue & Retention** (ARPU → revenue per converted user → engagement score)  
Engagement score improved significantly, but revenue per converted user dropped sharply. This is the key tension in the data.

**Guardrail Metrics** (refund rate, support ticket rate, days to convert, segment-level drops, revenue per converted user)  
These metrics flag potential harm. Two guardrails are elevated in Treatment.

---

## 4. Experiment Result Summary

| Metric | Control | Treatment | Lift | Significant? |
|---|---|---|---|---|
| User Count | 690 | 710 | +20 | — |
| Landing Page Visit Rate | 63.6% | 72.4% | +8.73pp | YES (p=0.0004) |
| Trial Start Rate | 25.1% | 29.0% | +3.94pp | No (p=0.097) |
| Onboarding Completion Rate | 15.7% | 21.1% | +5.49pp | YES (p=0.0083) |
| **Paid Conversion Rate (NS)** | **3.19%** | **7.04%** | **+3.85pp** | **YES (p=0.0011)** |
| Avg Revenue per User (ARPU) | $51.97 | $54.25 | +$2.28 | No (p=0.91) |
| Revenue per Converted User | $1,630 | $770 | -$860 | YES (p=0.006) |
| Refund Rate | 0.00% | 0.42% | +0.42pp | No (p=0.087) |
| Support Ticket Rate | 0.220 | 0.373 | +0.153 | YES (p<0.001) |
| Avg Engagement Score | 57.0 | 62.9 | +5.9 | YES (p<0.001) |
| Avg Days to Convert | 8.9 days | 6.4 days | -2.5 days | No (p=0.122) |

---

## 5. Hypothesis Test Interpretation

**Test:** Two-Proportion Z-Test (One-Tailed)  
**Null Hypothesis (H0):** Conversion rate (Treatment) ≤ Conversion rate (Control)  
**Alternate Hypothesis (H1):** Conversion rate (Treatment) > Conversion rate (Control)

**Z-Statistic: 3.264**  
**P-Value: 0.000549**  
**Decision: REJECT H0**

The result is statistically significant at the 5% level (and also at 1%). The 120.8% relative lift in paid conversion rate is not attributable to random variation. The Treatment campaign demonstrably drives more users to paid subscription.

---

## 6. Guardrail Metric Analysis

### Guardrail 1: Revenue per Converted User — ELEVATED RISK
Treatment converters generated $770 on average vs $1,630 in Control — a drop of 52.8%. This is statistically significant (p=0.006). While more users are converting, they are paying less. This could indicate:
- Treatment attracts lower-tier plan choosers
- Shorter trial periods (Treatment converts faster) reduce commitment
- Promotional pricing or discounts inflating conversion numbers

**Risk Level: HIGH** — This must be investigated before full launch.

### Guardrail 2: Support Ticket Rate — ELEVATED RISK
Treatment users generated support tickets at a rate 69% higher than Control (0.37 vs 0.22). This is statistically significant (p<0.001). Higher support volume signals friction, confusion, or unmet expectations in the new onboarding experience.

**Risk Level: HIGH** — Customer success costs will increase substantially at scale.

### Guardrail 3: Refund Rate — LOW RISK
Treatment had a refund rate of 0.42% vs 0.00% in Control. While any refunds are new (Control had none), the rate is very small in absolute terms and the difference is not statistically significant (p=0.087). This is a flag to monitor but not a blocker.

**Risk Level: LOW-MEDIUM** — Monitor post-launch.

### Guardrail 4: Days to Convert — POSITIVE SIGNAL
Treatment users convert 2.5 days faster (6.4 vs 8.9 days). Faster conversion is generally positive, suggesting the new campaign reduces friction early. However, it could also mean users are converting before fully understanding the product — which may contribute to the revenue and support signals above.

### Guardrail 5: Segment-Level Conversion — NO DECLINES
All regions and device types showed positive lift in Treatment. No segment experienced a conversion decline, which is a healthy signal with no harm to specific user groups.

---

## 7. Segment-Level Insights

**By Region:**
| Region | Control Conv. | Treatment Conv. | Lift |
|---|---|---|---|
| North | 3.5% | 8.9% | +5.4pp |
| South | 3.3% | 7.7% | +4.4pp |
| East | 2.5% | 6.5% | +4.0pp |
| West | 3.4% | 5.1% | +1.7pp |

North region shows the strongest lift. West shows the weakest response — worth monitoring.

**By Device Type:**
| Device | Control Conv. | Treatment Conv. | Lift |
|---|---|---|---|
| Mobile | 2.6% | 7.4% | +4.8pp |
| Desktop | 4.5% | 6.6% | +2.1pp |
| Tablet | 1.8% | 7.1% | +5.3pp |

Mobile and Tablet users show exceptional lift. The campaign appears particularly effective for non-desktop users.

**By Plan Type:**
| Plan | Control Conv. | Treatment Conv. | Lift |
|---|---|---|---|
| Free | 3.1% | 9.3% | +6.2pp |
| Basic | 3.6% | 3.9% | +0.3pp |
| Premium | 2.8% | 6.3% | +3.5pp |

Free plan users show the highest relative lift (+200%). The campaign is most effective at converting users on the free plan to paid.

**By Traffic Source:** All traffic sources show positive lift. Paid Search showed the strongest absolute improvement.

---

## 8. Final Recommendation: Conditional Launch

**Decision: LAUNCH — with phased rollout and active monitoring**

The data supports launching the Treatment campaign, with the following conditions:

**Phase 1 (Immediate):** Roll out to Free plan users on Mobile and Tablet. This segment shows the highest conversion lift and represents the lowest risk, as these users were not already paying.

**Phase 2 (30-day review):** Expand to all users, contingent on:
- Support ticket rate returning to within 20% of Control baseline
- Revenue per converted user improving above $1,000
- Refund rate remaining below 1%

**Do NOT yet:** Launch to Premium plan users without further investigation, as premium users converting at lower revenue-per-user values could indicate plan downgrade behaviour.

---

## 9. Risks and Limitations

1. **Revenue quality concern** — The drop in revenue per converted user is significant and must be explained. If Treatment converts users who quickly churn, the LTV impact could outweigh the conversion gain.
2. **Support cost escalation** — A 69% increase in support tickets will increase operational costs. At 10x scale, this is a material risk.
3. **Short observation window** — Data covers 30-day revenue. Long-term retention, churn, and LTV are unknown.
4. **Dataset had 8 duplicate user IDs** — These were removed. Root cause should be investigated.
5. **Missing device/traffic data** — 18 device and 24 traffic source values were null. These users were retained but excluded from segment-specific analysis.
6. **Experiment imbalance** — Treatment group (710) was slightly larger than Control (690), a 1.4% difference. This is acceptable but introduces minor noise.

---

## 10. Next Steps

| Action | Owner | Timeline |
|---|---|---|
| Investigate revenue per converted user drop | Analytics / Finance | 1 week |
| Audit support ticket categories (what are users asking?) | Customer Success | 1 week |
| Phase 1 launch to Free/Mobile segment | Engineering / Product | 2 weeks |
| Set up real-time monitoring dashboard | Analytics | 2 weeks |
| 30-day post-launch review of guardrail metrics | Business Analyst | 30 days |
| Evaluate 90-day retention and LTV of Treatment cohort | Analytics | 90 days |
| A/B test revised onboarding to reduce support tickets | Product | Next cycle |
