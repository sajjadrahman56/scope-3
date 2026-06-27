# The current problem

Traditional Scope 3 calculation is

> Scope 3 = Activity Data × Emission Factor

For example

| Activity            | Emission Factor     | Emission    |
| ------------------- | ------------------- | ----------- |
| $2M steel purchased | 2.3 kg CO₂e/USD     | 4,600 tCO₂e |
| 5000 km shipping    | 0.12 kg CO₂e/ton-km | 600 tCO₂e   |

The problem is:

* many companies don't know activity data
* suppliers don't report
* reports are incomplete
* emission factors are missing
* SMEs rarely publish Scope 3

So companies simply write

> "Not available"

or estimate using rough averages.

This is where ML becomes useful.

---

# Research Idea 1 (Best)

## Predict Missing Scope 3 Emissions

Instead of calculating directly,

train ML to estimate missing emissions.

Input features

* Industry
* Revenue
* Employees
* Country
* Scope 1
* Scope 2
* Energy use
* Purchased goods cost
* Logistics spending
* Capital expenditure
* Waste
* Business travel
* Supplier count

Output

Estimated Scope 3 emissions

Models

* Random Forest
* XGBoost
* CatBoost
* LightGBM

This is probably the strongest MSc project.

---

# Research Idea 2

## Predict whether a company is underreporting Scope 3

You already mentioned:

> firms don't report because

* reporting isn't worthwhile
* unable to report
* intentionally avoid reporting

That becomes a classification problem.

Input

* ESG score
* Company size
* Industry
* Country
* Profit
* Carbon policy
* Scope 1
* Scope 2

Output

Class

* Complete reporting
* Partial reporting
* No reporting

Models

* Random Forest
* XGBoost
* SVM

Novelty

AI detects companies likely hiding Scope 3 emissions.

---

# Research Idea 3

## Predict emission factors

Sometimes companies know

> purchased 100 tons steel

but don't know emission factor.

ML can predict

Emission Factor

using

* supplier country
* transport mode
* material type
* manufacturing process
* recycled content

instead of using average government factors.

---

# Research Idea 4

## Supplier Carbon Risk Score

Build ML that predicts

Supplier Risk

Features

Supplier

* country
* industry
* revenue
* electricity mix
* distance
* ESG score

Output

Carbon Risk

Low

Medium

High

Companies then prioritize high-risk suppliers.

This has real business value.

---

# Research Idea 5

## Deep Learning + NLP

Many companies publish

* Annual Reports
* Sustainability Reports
* ESG Reports

Instead of manually reading them,

use NLP.

Pipeline

PDF

↓

Text Extraction

↓

BERT

↓

Extract

* supplier emissions
* transport
* purchased goods
* waste

↓

Estimate Scope 3

Very few papers combine NLP and Scope 3 reporting.

---

# Research Idea 6

## Graph Neural Network (Very Novel)

Supply chains are graphs.

Company

↓

Supplier

↓

Supplier

↓

Factory

↓

Shipping

↓

Retail

Use Graph Neural Networks

Nodes

* companies

Edges

* supply relationships

Output

Carbon propagation through supply chain

Very advanced research.

---

# Research Idea 7

## Hybrid ML + GHG Protocol (Highly Recommended)

Don't replace the GHG Protocol.

Instead:

**Known data**

↓

GHG Formula

(Activity × Emission Factor)

**Missing data**

↓

ML Prediction

↓

Final Scope 3

This is much stronger than "pure ML" because it stays aligned with the standard while using AI only where data are unavailable. The GHG Protocol itself recognizes that companies often improve inventory quality over time and rely on different data sources and estimation methods. 

---

# A complete MSc-level workflow

```
Company Data
      │
      ▼
Cleaning
      │
      ▼
Feature Engineering
      │
      ▼
Missing Scope 3?
      │
 ┌────┴─────┐
 │          │
No         Yes
 │          │
GHG      ML Prediction
Formula      │
 │          │
 └────┬─────┘
      ▼
Total Scope 3
      ▼
Explainability (SHAP)
      ▼
Dashboard
```

---

# Where the novelty lies

Most existing work focuses on:

* calculating Scope 3 using emission factors,
* applying life-cycle assessment (LCA),
* or using economic input-output (EEIO) models.

There is much less research on **using machine learning to infer or estimate missing Scope 3 emissions from company characteristics and partial disclosures**. A contribution could be an **AI-assisted Scope 3 estimation framework** that combines GHG Protocol calculations with ML-based estimation for missing data, reducing reporting gaps while remaining transparent and explainable.

---

## Based on your project and datasets

Since you already have:

* the UK GHG Conversion Factors dataset,
* the GHG Protocol documentation,
* and are working on a Scope 3 emissions project,

I would recommend this research direction:

> **"An Explainable Machine Learning Framework for Estimating Missing Scope 3 Greenhouse Gas Emissions Using Corporate Activity Data and GHG Conversion Factors."**

This approach is practical, has a clear research gap, uses your available datasets, and allows you to compare multiple ML models (Random Forest, XGBoost, LightGBM) against traditional GHG Protocol calculations. Adding explainability methods such as SHAP would further strengthen the academic contribution by showing *why* the model predicts certain emissions, not just *what* it predicts.
