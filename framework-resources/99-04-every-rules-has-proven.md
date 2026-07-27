This is **exactly the question a supervisor or reviewer will ask**, and if we don't have a strong answer, BEACON will look subjective.

The answer is **yes and no**.

* **Yes**, there are proven sources for *how to define data quality rules*.
* **No**, there is **no existing document** that contains the exact rules for **Product Carbon Footprint (PCF)** datasets. Those rules are what BEACON contributes.

This distinction is very important.

---

# Where do validation rules come from?

They should **not** come from your opinion.

Instead, each rule should be derived from one (or more) of these sources:

### 1. International Standards ⭐⭐⭐⭐⭐

Examples:

* ISO/IEC 25012 (Data Quality Model)
* ISO 8000 (Data Quality)
* ISO 14067 (Product Carbon Footprint)
* GHG Protocol Product Standard

These tell you **what good-quality data should satisfy**, even if they don't write Python-style rules.

Example:

ISO 14067 requires transparent reporting of calculation methodology.

↓

BEACON Rule:

> Protocol Used for PCF must not be NULL.

---

### 2. Dataset Documentation ⭐⭐⭐⭐⭐

Example:

Carbon Catalogue paper and data descriptor.

If the dataset defines

> Product Weight is measured in kilograms.

↓

Rule

> Product Weight must use kg.

---

### 3. Domain Knowledge ⭐⭐⭐⭐

Example

Physics tells us

Weight cannot be negative.

↓

Rule

> Product Weight > 0

No paper is needed to prove gravity.

This is a domain constraint.

---

### 4. Business Rules ⭐⭐⭐⭐

Example

PCF values

Cannot be negative.

↓

Rule

PCF ≥ 0

Again

This comes from carbon accounting principles.

---

### 5. Statistical Rules ⭐⭐⭐

Example

Plausibility

No standard says

> "Use IQR."

Instead,

IQR is an accepted statistical method for outlier detection.

So

↓

Rule

Value should lie within acceptable statistical limits.

Implementation

↓

IQR

or

Modified Z-score

or

Isolation Forest

---

# So every rule should have a source

For example

| Rule                            | Source                                       |
| ------------------------------- | -------------------------------------------- |
| Product Weight must not be NULL | ISO/IEC 25012 (Completeness principle)       |
| Product Weight > 0              | Physical constraint / ISO 14067 context      |
| Unit must be kg                 | Carbon Catalogue documentation               |
| Protocol reported               | ISO 14067 + GHG Protocol                     |
| Year within reporting period    | Dataset documentation + Timeliness principle |
| Company not blank               | ISO/IEC 25012 Completeness                   |

Notice

Some rules come from standards.

Some from dataset documentation.

Some from science.

Some from statistics.

---

# This is where BEACON becomes original

The standards never say

| Feature        | Dimension    | Rule             |
| -------------- | ------------ | ---------------- |
| Product Weight | Completeness | Must not be NULL |
| Product Weight | Validity     | >0               |
| Product Weight | Consistency  | kg               |

**You create this mapping.**

So your contribution is **not inventing the rules from nothing**.

Your contribution is

> **systematically translating generic data quality principles, PCF standards, dataset specifications, and domain knowledge into a feature-level rule-based assessment framework for PCF datasets.**

That is academically acceptable.

---

# I actually recommend one more column

Instead of

| Feature | Dimension | Rule | Severity |

I would make it

| Feature | Dimension | Validation Rule | Rule Source | Justification |
| ------- | --------- | --------------- | ----------- | ------------- |

Example

| Feature        | Dimension    | Validation Rule  | Rule Source                     | Justification                                                    |
| -------------- | ------------ | ---------------- | ------------------------------- | ---------------------------------------------------------------- |
| Product Weight | Completeness | Must not be NULL | ISO/IEC 25012                   | Mandatory values are required for complete records.              |
| Product Weight | Validity     | Value > 0        | Physical constraint / ISO 14067 | Negative product weights are physically impossible.              |
| Protocol Used  | Traceability | Must be reported | ISO 14067; GHG Protocol         | The calculation methodology must be documented for transparency. |

---

## I would change one thing in our roadmap

Before writing the **Master Rule Book**, I think we should create a **Rule Source Matrix**.

This matrix defines the **allowed evidence** for BEACON rules:

| Rule Source             | Examples                                                      |
| ----------------------- | ------------------------------------------------------------- |
| International Standards | ISO/IEC 25012, ISO 8000, ISO 14067, GHG Protocol              |
| Dataset Documentation   | Carbon Catalogue data descriptor                              |
| Domain Constraints      | Physical laws, carbon accounting principles                   |
| Statistical Methods     | IQR, Modified Z-score, distribution checks                    |
| Literature              | Peer-reviewed papers supporting specific validation practices |

Then every rule in the Master Rule Book must cite **at least one** of these evidence sources. This will make BEACON much easier to defend because no rule will appear to be based solely on personal judgment. I would strongly recommend this approach for a dissertation or journal paper.
