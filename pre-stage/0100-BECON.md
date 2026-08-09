😂 Yes, I remember this very clearly. Actually, this was one of the biggest ideas we developed together. Your memory is mixing two versions of the project, so let me reconstruct it.

---

# Version 1 (Original DPP)

Your original project was

> **Scope 3 Carbon Emission Prediction via Machine Learning: A Data Quality Assessment Framework**

The idea was:

```
Raw Scope 3 data
        ↓
Data Quality Assessment
        ↓
Quality Segmentation
        ↓
Machine Learning
        ↓
Prediction Accuracy
        ↓
Decision Support
```

The framework name became

> **BEACON**
> (Business Emissions Assessment and Carbon Output Network)

Your DPP already reflects this idea. The objectives include designing a data quality framework, segmenting records into High/Medium/Low quality, comparing ML models, and measuring how data quality affects prediction accuracy. 

---

# Then we found the problem...

The biggest problem was

> **There is no free Scope 3 company-level dataset.**

Everything good was

* CDP → restricted
* Bloomberg → paid
* MSCI → paid
* Refinitiv → paid

Your supervisor therefore suggested

> Don't change the methodology.

Only change

> Scope 3 → another publicly available carbon dataset.

That was a very important decision.

---

# Then we started designing a framework

You asked me

> "Instead of only cleaning the data, can we create our own framework?"

My answer was

**Yes.**

That became

## BEACON

Instead of

```
Dataset
↓

Machine Learning
```

we proposed

```
Dataset

↓

BEACON Framework

↓

Machine Learning
```

meaning

BEACON becomes your contribution.

---

# Then PRISM appeared

Later we discussed another framework idea called

**PRISM**

It was **not** an existing published framework.

It was a working name for a methodology we were brainstorming.

The idea was

```
Stage 1

Data Quality Scoring (DQS)

↓

Stage 2

Machine Learning Prediction
```

The description you wrote:

> PRISM is a two-stage pipeline...

is almost exactly what we discussed.

---

The first stage was

```
Missing values

Consistency

Completeness

Reliability

Freshness

Uniqueness

↓

Weighted Score

↓

Data Quality Score
```

Every record receives

```
DQS = 0–100
```

---

Then

```
High Quality

Medium Quality

Low Quality
```

instead of random train/test.

---

Then Stage 2

Train

* Linear Regression

* Random Forest

* XGBoost

* ANN

* LSTM

Compare

RMSE

MAE

R²

---

# Then we realized something

PRISM was actually only

> a methodology.

BEACON sounded much stronger as a dissertation contribution.

So we decided

BEACON should be the framework.

Inside BEACON

there can be

Data Quality Scoring

Quality Segmentation

Prediction

Decision Support

---

# So BEACON became

Instead of

```
PRISM

↓

ML
```

we changed to

```
BEACON

Stage 1
Data Quality Assessment

↓

Stage 2
Quality Segmentation

↓

Stage 3
Prediction

↓

Stage 4
Decision Support
```

Exactly like your DPP says. 

---

# After changing the dataset...

Now that Scope 3 is gone,

BEACON still works.

Actually even better.

Now

```
Carbon Dataset

↓

BEACON

↓

Machine Learning

↓

Carbon Footprint Prediction
```

No dependency on Scope 3 anymore.

---

# What I would improve today (July 2026)

Now that we've found **The Carbon Catalogue**, I would redesign BEACON slightly.

```
                 BEACON Framework

                ┌─────────────────────┐
                │ Stage 1             │
                │ Data Quality Audit  │
                │                     │
                │ • Missing values    │
                │ • Completeness       │
                │ • Consistency        │
                │ • Outliers           │
                │ • Reliability        │
                └──────────┬──────────┘
                           │
                           ▼
                ┌─────────────────────┐
                │ Stage 2             │
                │ Data Quality Score  │
                │ (DQS)               │
                │                     │
                │ High                │
                │ Medium              │
                │ Low                 │
                └──────────┬──────────┘
                           │
                           ▼
                ┌─────────────────────┐
                │ Stage 3             │
                │ ML Prediction       │
                │                     │
                │ Linear Regression   │
                │ Random Forest       │
                │ XGBoost             │
                │ CatBoost            │
                │ ANN                 │
                └──────────┬──────────┘
                           │
                           ▼
                ┌─────────────────────┐
                │ Stage 4             │
                │ Evaluation          │
                │                     │
                │ RMSE                │
                │ MAE                 │
                │ R²                  │
                │ SHAP                │
                └──────────┬──────────┘
                           │
                           ▼
                Decision Support
```

---

## I think this is the key thing you've forgotten

Your dissertation was **never about inventing a new machine learning algorithm**.

The novelty was always:

> **Can a systematic Data Quality Framework (BEACON) improve carbon emission prediction compared with using raw data?**

The ML models are simply the tools used to test that hypothesis.

Now that you've found the Carbon Catalogue dataset, I actually think this original research idea is still valid. The only major change is that instead of focusing specifically on **Scope 3 emissions**, you'll focus on **product carbon footprint (PCF/CO₂e) prediction**, while keeping BEACON as the central contribution. That makes the project much easier to complete with openly available, academically credible data.
