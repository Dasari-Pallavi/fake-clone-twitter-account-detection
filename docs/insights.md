# Business Insights & Actionable Recommendations

## 1. Synthetic Baseline Parity Across Account Segments
* **Observation:** Across **50,000** accounts analyzed, the overall fake/bot rate is **50.04%**, with near-identical verification rates (**49.88%** bots vs. **50.14%** humans), average follower counts (**4,991.9** vs. **4,985.3**), and average engagement (**52.5** for both groups).
* **Implication:** Because the Kaggle dataset was generated synthetically with uniform distributions, standard supervised models perform near random chance (**49.0%** Logistic Regression accuracy; **50.0%** Random Forest accuracy).
* **Action:** Do not deploy automated permanent account bans based on these thresholds alone; recalibrate the classification pipeline on live production telemetry (such as posting frequency bursts, IP/device logs, and follower graph networks) before automation.

## 2. Out-of-Fold Probability Clustering & Risk Tier Routing
* **Observation:** Out-of-fold cross-validation (`Random Forest`) scored all **50,000** accounts without overfitting, clustering predicted probabilities tightly around `0.40–0.74`. As a result, **50.3%** of accounts fell into **Low - no action** (`<= 0.50`), **49.7%** fell into **Medium - manual review** (`0.50–0.80`), and **0.0%** crossed the strict `> 0.80` **High - priority review** cutoff.
* **Implication:** Static probability cutoffs (`0.80`) can leave the priority queue empty when model confidence is conservative or data distributions are uniform.
* **Action:** Implement dynamic capacity-based thresholds (for example, routing the **top 5%–10% highest probability scores** into the priority queue each week) so Trust & Safety reviewers always work on the highest-relative-risk profiles first.

## 3. Behavioral Clone Cluster Isolation via Euclidean Distance
* **Observation:** Standardizing all 11 behavioral features and applying pairwise Euclidean distance (`NearestNeighbors`) isolated **1,001** suspected clone-like accounts falling at or below the 2nd percentile distance cutoff (`<= 0.3858`).
* **Implication:** Accounts sitting at near-zero behavioral distance exhibit virtually identical activity footprints, making them strong candidates for coordinated bot networks or templated account creation.
* **Action:** Route `outputs/clone_pairs.csv` to investigators in paired batches (`username` alongside `nearest_user`) rather than isolated single-account tickets to speed up network triage.
