# Business Problem Statement

## 1. Background & Business Problem
Social media platforms experience significant operational, financial, and user-trust risks caused by fake (automated bot) and cloned accounts. These accounts artificially inflate engagement metrics, distribute spam, and impersonate legitimate users. Manually auditing all 50,000+ accounts is unscalable for Trust & Safety operations teams.

## 2. Stakeholders
* **Primary Stakeholders:** Trust & Safety Operations Team, Risk & Fraud Analysts.
* **Secondary Stakeholders:** Platform Integrity Managers, Product Analytics Leadership.

## 3. Project Objective
Design a structured, data-driven decision support prototype that:
1. Benchmarks behavioral KPIs separating genuine users from automated profiles.
2. Evaluates classification models to estimate fake account probability while balancing false positives against missed threats.
3. Identifies near-duplicate "clone" accounts using Euclidean distance similarity so analysts can review coordinated accounts in batches.
4. Segments accounts into **Low, Medium, and High Operational Risk Tiers** to prioritize manual review queues.

## 4. Success Metrics
* **Model Evaluation:** Precision, Recall, and F1-Score on the fake/bot class (`bot_label = 1`).
* **Operational Efficiency:** Percentage of total accounts diverted away from unnecessary manual review (`Low - no action` tier) and number of behaviorally similar clone pairs isolated for batch investigation.

## 5. Scope & Constraints
* **Dataset:** [Twitter-Bot Detection Dataset on Kaggle](https://www.kaggle.com/datasets/goyaladi/twitter-bot-detection-dataset) (`50,000` simulated account records).
* **Scope:** End-to-end analytical prototype demonstrating KPI engineering, classification, Euclidean similarity scoring, risk tiering, and Power BI dashboarding.
