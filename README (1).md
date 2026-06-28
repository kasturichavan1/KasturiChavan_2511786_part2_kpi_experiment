# Part 2 – KPI Framework, Business Experiment Analysis & Decision Recommendation

## What is this project about?

A digital subscription company ran an experiment to see if a new onboarding campaign would get more users to sign up for a paid plan.

They split users into two groups:
- **Control** – users who saw the old onboarding experience
- **Treatment** – users who saw the new campaign

My job was to analyse the results and tell leadership whether they should roll out the new campaign to everyone.

---

## What data was used?

The dataset had **1,408 users** with information like:
- Which group they were in (Control or Treatment)
- Whether they visited the landing page, started a trial, completed onboarding, or paid
- How much revenue they generated
- Whether they raised a support ticket or asked for a refund
- Their engagement score
- How many days it took them to convert

---

## What metric did I focus on? (North Star)

I chose **Paid Conversion Rate** as the main success metric — basically, what percentage of users actually became paying customers.

This is the most important metric because the whole point of the campaign is to get more people to pay. Everything else (visits, trials, onboarding) is just a step along the way.

---

## KPI Tree

I broke down the main metric into smaller drivers to understand what moves it:

- **Acquisition** – are users even finding the landing page?
- **Activation** – are users completing onboarding and starting a trial?
- **Revenue** – are the users who convert actually generating good revenue?

I also tracked **guardrail metrics** — things that should NOT get worse even if conversion goes up:
- Refund rate
- Support ticket rate
- Revenue per converted user

---

## What did the experiment show?

| Metric | Control | Treatment |
|---|---|---|
| Paid Conversion Rate | 3.2% | 7.0% |
| Onboarding Completion | 15.7% | 21.1% |
| Engagement Score | 57.0 | 62.9 |
| Revenue per Converted User | $1,630 | $770 |
| Support Ticket Rate | 0.22 | 0.37 |

The Treatment group converted way more users — but they also generated fewer revenue per person and raised way more support tickets.

---

## Was the result statistically significant?

Yes. I ran a **Two-Proportion Z-Test** on the conversion rate:

- Z-score = **3.264**
- P-value = **0.00055**
- This is way below the 0.05 threshold, so the result is real and not just luck

---

## Guardrail Check

Two things concerned me about the Treatment group:

1. **Revenue per converted user dropped by 53%** – people are converting but paying less
2. **Support tickets went up 69%** – more users are running into problems

These are red flags that need to be looked into before going all-in on the new campaign.

---

## My Recommendation

**Launch it — but slowly.**

- Start by rolling it out to **Free plan users on Mobile and Tablet** (they showed the biggest improvement)
- Watch the guardrail metrics closely for 30 days
- Only expand to all users once the support ticket and revenue issues are explained

---

## Files in this repo

| File | What it is |
|---|---|
| `data/campaign_experiment_data.xlsx` | The raw dataset |
| `analysis/experiment_analysis.xlsx` | Data cleaning, full analysis, and hypothesis test |
| `analysis/hypothesis_test_notes.md` | Explanation of the statistical test I ran |
| `outputs/kpi_tree.png` | Visual diagram of the KPI tree |
| `outputs/experiment_summary.xlsx` | Summary table comparing Control vs Treatment |
| `outputs/recommendation_memo.md` | Full write-up of my recommendation |
| `screenshots/summary_metrics.png` | Screenshot of the metrics table |
| `screenshots/hypothesis_test_output.png` | Screenshot of the hypothesis test results |
| `screenshots/kpi_tree_preview.png` | Screenshot of the KPI tree |

---

## Assumptions I made

- Duplicate user IDs (8 of them) were removed — kept the first record
- Missing device and traffic source values were kept in but excluded from those specific segment breakdowns
- Revenue outliers were kept in since they look like genuine premium users
- The 30-day window means we don't know about long-term retention yet
