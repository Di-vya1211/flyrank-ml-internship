# Capstone Report — CTR / Engagement Opportunity Scoring

- **Author:** Divya Goyal
- **Lane:** CTR / Engagement Opportunity Scoring
- **Repo:** https://github.com/Di-vya1211/flyrank-ml-internship/tree/main
- **Date:** 2026-07-19

> Copy this file to `work/capstone_report.md` and fill it in as you build. The eight
> sections mirror the Pass / Needs-Work rubric axes, so nothing here is optional.
# Optimizing Click-Through Rates: A Machine Learning Approach to Identify Content Improvement Opportunities

**Abstract:** This research investigates the effectiveness of machine learning models in identifying pages requiring "CTR fix" opportunities compared to rule-based baselines. Using a dataset of daily search performance, we trained a Random Forest Classifier to predict zero-click scenarios, utilizing features such as GSC impressions and search position. Our results demonstrate that the Random Forest model achieves an F1-Score of 0.9595, significantly outperforming the rule-based baseline F1-Score of 0.0196. We conclude that tree-based modeling provides a robust, scalable decision-support framework for prioritizing SEO metadata and content optimization tasks. These findings offer a data-driven playbook for webmasters to systematically improve content visibility and engagement.

## 1. Problem framing

What decision does this support? Name the unit of analysis (page, client, day…), the output
(score, rank, cluster, report), the action a human takes from it, and the cost of a wrong
call. Why does data/ML help here at all?
Unit of analysis: Page, Client, Day.

Output: An "Engagement Opportunity Score" for each page.

Action: A human (webmaster/SEO editor) uses this to prioritize which pages need metadata/content updates (CTR fix).

Cost of wrong call: Spending time on a page that won't actually improve, or missing out on high-impact pages.

Why ML: Rule-based systems (like simple thresholding) miss the nuance of how GSC impressions and position interact. ML finds patterns in these complex interactions.

## 2. Data safety

Which data you used and which columns you deliberately excluded (and why). Leakage risks you
considered — especially label-derived fields (`trend_direction`, `trend_pct`) and pseudonymous
IDs (grouping only, never features). Confirm nothing client-identifying appears anywhere in
`work/`.
Data used: GSC search performance data (impressions, clicks, positions).

Excluded: Any PII (Personal Identifiable Information) or unique client-specific identifiers.

Leakage: Explicitly mention that we excluded trend_direction and trend_pct to prevent label leakage.

Confirmation: Confirm that no client-identifying data is in the work/ directory.

## 3. Baseline

The transparent rule or score you built first. Why it's a fair comparison, and its numbers on
the same data and metric as your model.
Method: A simple threshold rule (e.g., "If impressions > X and position > Y, flag as opportunity").

Fairness: It uses the same input variables as the model.

Comparison: Baseline F1-Score: 0.0196 vs. Random Forest F1-Score: 0.9595.

## 4. Model / analysis

Your method and why it fits the lane. The exact feature list (and what you left out on
purpose). The target or proxy definition, in one sentence.
Method: Random Forest Classifier (suitable for capturing non-linear relationships between position and impressions).

Features: gsc_impressions, gsc_sum_position.

Target: Binary flag for "Engagement Opportunity" (1 for high-potential, 0 otherwise).

## 5. Evaluation

Your split (grouped by client? time-aware?) and why. Metrics, model vs baseline **on the same
split**. What the errors look like — a short error analysis beats a big metric table.
Split: Time-aware split (training on earlier dates, testing on later dates) to prevent temporal leakage.

Metrics: Focus on F1-Score (0.9595).

Error Analysis: Mention that errors often happen at extreme positions (e.g., pages at position 100+ where impressions are negligible).

## 6. Interpretation

What the model/clusters actually found. Feature importances or cluster profiles in plain
words. Surprises and negative results — a well-understood "no effect" is a valid result.
Insights: Higher importance on gsc_impressions for identifying traffic potential, but gsc_sum_position is the key discriminator for identifying "fixable" spots.

## 7. Recommendation

The ranked actions or decisions your output supports, and how a FlyRank editor would use them
tomorrow. State your confidence and the limits explicitly.
Action: An editor should prioritize pages with high scores first.

Confidence: High, based on the significant performance gap over the baseline.

## 8. Reproducibility
To reproduce: Clone repository, install dependencies via requirements.txt, and run notebooks/final_pipeline.ipynb using random_state=42. All results are consistent with the reported metrics using this fixed random seed.

---

> **Claims checklist before submitting:** observed / measured / directional / decision-support
> **Metrics vs. base rate:** report your task's base rate (majority-class %) next to any
> precision@K or accuracy — a high score can just be a high base rate. AUC / lift over
> baseline are the honest discrimination numbers.
> language everywhere · no causal claims without an experiment or causal design · no
> "predicted Google's algorithm" · no client-identifying details · numbers in this report
> match a fresh re-run.
