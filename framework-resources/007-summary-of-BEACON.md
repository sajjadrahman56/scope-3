# Proposal: BEACON Framework

### **BEACON: A Data Quality Assessment and Validation Framework for Product Carbon Footprint (PCF) Datasets**

## Why are we developing BEACON?

Current PCF datasets (e.g., Carbon Catalogue) are widely used for machine learning and carbon footprint prediction, but there is **no standard framework to systematically assess and validate their data quality**.

Existing studies focus on:

* Data cleaning
* Missing value handling
* ML model performance

However, they rarely answer:

> **"How good is the dataset before training the ML model?"**

BEACON aims to fill this gap.

---

# Main Objective

Develop a **PCF-specific Data Quality Framework** that can:

1. Assess the quality of existing PCF datasets.
2. Validate newly collected PCF data before adding it to a dataset.
3. Produce an overall Data Quality Score.
4. Recommend improvements.
5. Evaluate whether a dataset is suitable for ML-based PCF prediction.

---

# Proposed Workflow

```text
PCF Dataset
      │
      ▼
Feature → Dimension Mapping
      │
      ▼
Quality Assessment
      │
      ▼
Dimension Scores
      │
      ▼
Overall BEACON Score
      │
      ▼
Quality Report
      │
      ▼
Cleaning Recommendations
      │
      ▼
ML Ready Dataset
```

---

# Proposed Data Quality Dimensions

Initially we can use eight dimensions.

| Dimension          | Purpose                                                           |
| ------------------ | ----------------------------------------------------------------- |
| Completeness       | Are required values missing?                                      |
| Accuracy           | Are values correct and realistic?                                 |
| Consistency        | Are formats and units consistent?                                 |
| Validity           | Do values satisfy predefined rules?                               |
| Traceability       | Can the data source be identified?                                |
| Timeliness         | Is the information sufficiently recent?                           |
| Interpretability   | Are the data understandable and well documented?                  |
| Representativeness | Does the dataset represent different products and sectors fairly? |

These dimensions are adapted from existing data quality literature but customised for PCF datasets.

---

# Feature → Dimension Mapping

Each dataset feature will be evaluated using one or more quality dimensions.

Example:

| Feature        | Completeness | Accuracy | Consistency | Traceability |
| -------------- | ------------ | -------- | ----------- | ------------ |
| Product Weight | ✓            | ✓        | ✓           | ✓            |
| PCF            | ✓            | ✓        | ✓           | ✓            |
| Protocol       | ✓            | ✓        | ✓           | ✓            |
| Country        | ✓            | ✓        | ✓           | ✓            |

This mapping defines which quality dimensions are relevant for each feature.

---

# Dimension Metrics

Each dimension will have measurable rules.

Example:

### Completeness

Missing Rate

```text
Completeness = Non-missing / Total
```

---

### Accuracy

Examples:

* Weight > 0
* PCF > 0
* Carbon Intensity ≥ 0

---

### Consistency

Examples:

* All weights stored in kg
* Country names follow one standard
* CO₂ values use the same unit

---

### Traceability

Examples:

* Weight source available
* Protocol reported
* Data origin documented

---

# BEACON Score

Each dimension produces a score between 0–100.

Example

| Dimension          | Score |
| ------------------ | ----: |
| Completeness       |    96 |
| Accuracy           |    91 |
| Consistency        |    88 |
| Validity           |    97 |
| Traceability       |    72 |
| Timeliness         |    83 |
| Interpretability   |    95 |
| Representativeness |    81 |

↓

Overall

```text
BEACON Score = 88.6 / 100
```

---

# Dataset Classification

Example

|    Score | Quality   |
| -------: | --------- |
|   90–100 | Excellent |
|    80–89 | Good      |
|    70–79 | Fair      |
| Below 70 | Poor      |

---

# Recommendations

BEACON should not only assign scores but also generate recommendations.

Example

| Problem                       | Recommendation                     |
| ----------------------------- | ---------------------------------- |
| Missing Protocol              | Report ISO/GHG Protocol used       |
| Weight Source Missing         | Add supplier or measurement source |
| Country Format Inconsistent   | Convert to ISO country names       |
| Missing End-of-Life Emissions | Include end-of-life assessment     |

---

# Future Validation Module

BEACON should also validate new data before insertion.

Workflow

```text
New Record
      │
      ▼
BEACON Validation
      │
 ┌────┴────┐
 │         │
PASS     FAIL
 │         │
 ▼         ▼
Database  Error Report
```

Example

```
Weight = -20 kg

❌ Invalid
```

```
Protocol = NULL

❌ Missing
```

```
Country = U.S.A

⚠ Standardise to USA
```

This allows BEACON to act as a quality gate for future PCF datasets.

---

# Machine Learning Validation

We can also investigate whether improving data quality improves ML performance.

Example

| Stage           | BEACON Score | ElasticNet R² |
| --------------- | -----------: | ------------: |
| Before Cleaning |           69 |          0.72 |
| After Cleaning  |           91 |          0.84 |

If model performance improves after data quality improvements, this strengthens the practical value of BEACON.

---

# Expected Contributions

If successfully developed, BEACON could contribute:

1. A **PCF-specific Data Quality Framework**, rather than a generic one.
2. A **Feature-to-Dimension Mapping Matrix** for PCF datasets.
3. **Measurable quality metrics** for each data quality dimension.
4. A **BEACON Quality Score** (0–100) to quantify dataset quality.
5. A **Validation Framework** for screening new PCF records before they are added to a dataset.
6. **Actionable recommendations** to improve data quality.
7. An evaluation of how **data quality influences ML-based PCF prediction**.

---

## One important suggestion before starting

আমি টিমকে একটা কথা অবশ্যই বলতাম:

> **এগুলো এখনো research ideas, final framework না।** প্রথমে literature review করতে হবে—দেখতে হবে PCF data quality নিয়ে আগে কী হয়েছে, generic data quality frameworks (যেমন ISO 25012, Wang & Strong, AI Act) কী বলে, এবং কোন অংশে সত্যিকারের research gap আছে। এরপর BEACON-এর dimensions, metrics এবং scoring methodology evidence-এর ভিত্তিতে refine করতে হবে।

এভাবে এগোলে framework-এর novelty এবং publishability দুটোই অনেক বেশি শক্তিশালী হবে।
