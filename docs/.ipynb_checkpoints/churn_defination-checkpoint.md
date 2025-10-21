# churn_definition.md

## 1. Project Overview

**Project Name:** Customer Churn Analysis & Dashboard
**Purpose:**
This document defines customer churn for the project, specifies KPIs, and provides guidelines for calculating, tracking, and interpreting churn. The goal is to enable consistent measurement, identify at-risk customers, and inform retention strategies.

## 2. Churn Definition

**Business Definition:**
A customer is considered **churned** if they stop using our service or cancel their subscription within a defined period.

**Example Rules:**

* **SaaS Subscription:** Subscription not renewed within **30 days** of expiration.
* **Telecom / Utilities:** No payment or usage activity for **60 consecutive days**.
* **E-commerce / Retail:** No purchase activity for **12 months**.

**Edge Cases:**

* Paused or trial subscriptions are considered **active**.
* Customers requesting refunds are considered churned if they do not renew.

## 3. Data Sources

| Table / Source        | Columns Used                                          | Notes                                      |
| --------------------- | ----------------------------------------------------- | ------------------------------------------ |
| `customers.csv`       | `customer_id`, `join_date`, `churn_date`, `is_active` | Primary source for churn flags             |
| `subscriptions.csv`   | `plan_type`, `last_payment_date`                      | Identify lapsed subscriptions              |
| `usage_logs.csv`      | `last_login_date`, `login_count_30_days`              | Detect inactivity                          |
| `support_tickets.csv` | `ticket_date`, `issue_type`, `resolution_time`        | Optional: support-related churn indicators |

## 4. Churn Calculation Logic

**Formula:**

```
Churn Rate (%) = (Number of churned customers in period / Total customers at start of period) * 100
```

**Step-by-Step Logic:**

1. Identify active customers at the start of the period.
2. Apply churn definition rules (inactivity, cancellations, non-renewals).
3. Count churned customers.
4. Calculate churn rate using the formula above.

**Thresholds:**

* Inactivity ≥ 60 days → churned
* Subscription canceled or not renewed → churned

## 5. KPIs / Metrics

| KPI                           | Formula                                                | Frequency           |
| ----------------------------- | ------------------------------------------------------ | ------------------- |
| Customer Churn Rate           | `(Churned Customers ÷ Total Customers at Start) × 100` | Monthly / Quarterly |
| Revenue Churn                 | `(Lost Revenue ÷ Total Revenue) × 100`                 | Monthly             |
| Retention Rate                | `(Active Customers ÷ Total Customers at Start) × 100`  | Monthly             |
| Customer Lifetime Value (CLV) | `Avg. Revenue × Avg. Customer Lifespan`                | Quarterly           |

## 6. Segmentation Rules

Churn will be analyzed by:

* **Region:** e.g., North, South, East, West
* **Plan Type:** Basic, Standard, Premium
* **Customer Segment:** Individual, SMB, Enterprise
* **Product / Service Line**

## 7. Business Assumptions

* Paused subscriptions are considered **active**.
* Minimum tenure to be considered “active customer” = 1 month.
* Churn is tracked **monthly**, aligned with reporting periods.
* Partial refunds or discounts do not prevent a churn designation if the customer leaves.

## 8. Versioning & Ownership

| Version | Date       | Author              | Changes                               |
| ------- | ---------- | ------------------- | ------------------------------------- |
| 1.0     | 2025-10-12 | Venkat              | Initial definition                    |
| 1.1     | TBD        | TBD                 | Updates based on stakeholder feedback |

**Owner / Contact:**

* Name: Venkat Reddy N
* Email: [rikhithreddy@gmail.com]

