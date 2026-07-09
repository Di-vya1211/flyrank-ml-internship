# ML Task Framing: Content Refresh Optimization

## 1. Task Type
* **Type:** Ranking / Scoring
* **Explanation:** We are scoring and ranking web pages to identify which specific content is currently declining in performance and requires an editor's review or a refresh.

## 2. Target or Proxy
* **Target:** `is_declining_label`
* **Explanation:** A binary indicator (1 or 0) derived from the `trend_direction` feature being "down", which acts as our ground truth proxy for performance decay.

## 3. Success Metric
* **Metric:** Precision@50 (and Precision@20)
* **Explanation:** Out of the top 50 pages our model flags as "declining," we measure what fraction are actually declining. Higher precision ensures content editors don't waste time reviewing healthy pages.

## 4. Real Content Action Supported
* **Action:** Prioritized Content Refresh Workflow
* **Explanation:** The output directly powers a dashboard for the content operations team, allowing them to instantly target and update the most critically stale, high-exposure pages to reclaim lost traffic.

## 5. Why ML Beats a Fixed Rule
* **Explanation:** While a manual hand rule (like combining staleness and visibility thresholds) performs decently at the very top (Precision@20), it quickly loses signal and drops accuracy deeper down. A machine learning model like a Decision Tree automatically discovers non-linear relationships across multiple features (impressions, average position, content age) simultaneously, sustaining higher precision (Precision@50) without manual, tedious threshold tuning.
