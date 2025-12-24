# specialty-therapy-discontinuation-case-study
End-to-end data science case study to predict near-term therapy discontinuation for a specialty treatment. Uses point-in-time feature engineering, interpretable modeling, and business-focused outputs to prioritize high-risk patients for proactive field support interventions.
# ProcDNA Discontinuation Risk Case Study

## Overview

This repository contains an end-to-end data science case study focused on predicting **near-term (60-day) therapy discontinuation risk** for patients on a high-touch specialty therapy.

Staying on therapy depends on multiple coordinated steps such as payer approval, specialty pharmacy shipments, patient affordability, and timely follow-ups. Patients can appear stable at one point in time and then suddenly discontinue due to access friction (e.g., denied refills, high out-of-pocket costs, missed follow-ups).

The goal of this project is to build a **data-driven early warning model** that helps Analytics & Insights and field support teams **prioritize high-risk patients** for proactive intervention, given limited outreach capacity.

---

## Problem Statement

Given longitudinal patient activity and contextual data at a defined **prediction anchor point**, predict whether a patient is likely to discontinue therapy within the next 60 days.

The solution must:
- Use **only information available at or before the prediction anchor**
- Produce **interpretable drivers** of risk
- Generate **actionable outputs** that field teams can act on

---

## Data Sources

The analysis uses three de-identified input tables:

### 1. `events_status_shipments.csv`
Longitudinal, patient-level event data including:
- Referrals and access milestones
- Status changes and payer transitions
- Shipments, refills, and rejected refills
- Support interactions

Each patient has a single row flagged as `is_prediction_anchor = 1`, which represents the point in time when the patient is scored.  
The binary label `discontinued_within_60d` indicates whether the patient discontinued therapy within 60 days after the anchor.

### 2. `hcps_master.csv`
Site-level attributes for treating practices, such as:
- Site type and specialty bucket
- Region
- Historical discontinuation behavior
- Engagement with patient support programs

### 3. `payers_master.csv`
Payer and plan-level attributes, including:
- Channel and plan type
- Coverage posture and step therapy requirements
- Cost share levels
- Typical access and approval behavior

> **Note:** All identifiers and categorical fields are anonymized. Dates are preserved to enable meaningful time-based feature engineering.

---

## Methodology

The project follows a structured analytics workflow:

1. **EDA & Data Cleaning**
   - Distribution checks, missingness analysis, and time-based patterns
   - Reasoned handling of missing and inconsistent values

2. **Point-in-Time Feature Engineering**
   - Refill cadence and shipment gaps
   - Access friction signals (rejections, delays, payer changes)
   - Site- and payer-contextual risk indicators  
   - Strict prevention of label leakage by excluding post-anchor information

3. **Feature Prioritization**
   - Logical and domain-driven feature selection
   - Reduction to a manageable and interpretable feature set

4. **Modeling & Evaluation**
   - Baseline classifier for reference
   - Stronger machine learning model for improved discrimination
   - Evaluation using ranking and classification metrics

5. **Drivers & Interpretation**
   - Identification of key drivers influencing discontinuation risk
   - Plain-language explanations supported by visualizations

6. **Business Actionability**
   - Generation of a prioritized high-risk patient list
   - Clear guidance on how field support teams should act on the output

---

## How to Run the Project

### Prerequisites
- Python 3.9+
- Recommended: virtual environment

### Install dependencies
```bash
pip install -r requirements.txt

