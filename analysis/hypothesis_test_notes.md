# Hypothesis Test Notes
## Experiment: New Onboarding & Activation Campaign

---

## 1. Business Context

The company launched a new onboarding and activation campaign (Treatment) against the existing experience (Control). Leadership must decide whether to roll out the Treatment to all users. The hypothesis test is designed to determine whether the observed improvement in paid conversion rate is statistically significant, or could be due to random chance.

---

## 2. Metric Being Tested

**Paid Conversion Rate** — the proportion of users in each group who converted to a paid subscription within 30 days.

This is the North Star Metric because it directly measures revenue-generating behaviour and is the clearest signal of whether the new campaign achieves its core objective.

---

## 3. Hypotheses

| | Statement |
|---|---|
| **Null Hypothesis (H0)** | The paid conversion rate for the Treatment group is less than or equal to the paid conversion rate for the Control group. Conversion(Treatment) ≤ Conversion(Control) |
| **Alternate Hypothesis (H1)** | The paid conversion rate for the Treatment group is greater than the paid conversion rate for the Control group. Conversion(Treatment) > Conversion(Control) |

---

## 4. Test Design

| Parameter | Value |
|---|---|
| **Test Type** | Two-Proportion Z-Test (One-Tailed) |
| **Direction** | Right-tailed (testing for improvement in Treatment) |
| **Significance Level (α)** | 0.05 |
| **Confidence Level** | 95% |
| **Decision Rule** | Reject H0 if Z-statistic > 1.645 AND p-value < 0.05 |

**Why one-tailed?** The business question is directional: we only care whether the Treatment is *better* than Control, not just different. A one-tailed test provides more statistical power in the direction of interest.

**Why Z-test?** Both sample sizes exceed 30 (n1=690, n2=710), and the binary outcome (converted / not converted) meets the conditions for a normal approximation to the binomial distribution.

---

## 5. Test Inputs

| Input | Control | Treatment |
|---|---|---|
| Group Size (n) | 690 | 710 |
| Conversions (x) | 22 | 50 |
| Conversion Rate (p) | 3.19% | 7.04% |

---

## 6. Calculations

**Step 1 — Pooled Proportion:**
```
p_pool = (x1 + x2) / (n1 + n2)
p_pool = (22 + 50) / (690 + 710) = 72 / 1400 = 0.051429
```

**Step 2 — Standard Error:**
```
SE = sqrt(p_pool × (1 - p_pool) × (1/n1 + 1/n2))
SE = sqrt(0.051429 × 0.948571 × (1/690 + 1/710))
SE = sqrt(0.051429 × 0.948571 × 0.002823)
SE = sqrt(0.000138)
SE = 0.011749
```

**Step 3 — Z-Statistic:**
```
Z = (p2 - p1) / SE
Z = (0.0704 - 0.0319) / 0.011749
Z = 0.0385 / 0.011749
Z = 3.2640
```

**Step 4 — P-Value (one-tailed):**
```
P-value = P(Z > 3.264) = 1 - Φ(3.264)
P-value = 0.000549
```

---

## 7. Test Output

| Result | Value |
|---|---|
| **Z-Statistic** | 3.2640 |
| **Critical Z (α=0.05, one-tail)** | 1.645 |
| **P-Value (one-tailed)** | 0.000549 |
| **Significance Level** | 0.05 |
| **Decision** | **REJECT H0** |

---

## 8. Interpretation

**Statistical Interpretation:**
The Z-statistic of 3.264 exceeds the critical value of 1.645, and the p-value of 0.000549 is far below the significance threshold of 0.05. There is therefore strong statistical evidence to reject the null hypothesis.

**Business Interpretation:**
The Treatment group achieved a paid conversion rate of 7.04% compared to 3.19% in the Control group — a relative improvement of +120.8% (absolute lift of +3.85 percentage points). This improvement is statistically significant at the 95% confidence level and is very unlikely to have occurred by chance (probability < 0.055%).

The new onboarding and activation campaign demonstrably improves the proportion of users who convert to paid subscribers. This finding is robust and supports moving toward a launch decision, subject to guardrail metric evaluation.

---

## 9. Connection to Business Decision

This test directly informs the launch/no-launch decision. Because:
- The primary success criterion (paid conversion rate) improved significantly
- The result is unlikely to be noise (p < 0.001)
- The effect size is commercially meaningful (+3.85pp on a 3.19% baseline = +120.8%)

However, the hypothesis test alone is not sufficient. See `outputs/recommendation_memo.md` for the full decision framework incorporating guardrail metrics and segment analysis.
