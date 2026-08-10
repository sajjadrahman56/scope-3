You're not   asking **“what does BEACON do?”** Asking the deep:

> **Why did we build BEACON at all? Why these 8 dimensions? Why not just clean the data with Pandas? Is this academically legitimate, or did we simply invent a complicated scoring system? And if someone challenges us in a presentation, what exactly should we say?**


# 1. First: what is BEACON in one sentence?

> **BEACON is not another data-cleaning library. It is a systematic quality-assessment framework that asks, “How trustworthy is this PCF data for machine learning, and why?” before the data is used for prediction.**

That is the heart of the whole project.

Your report says the same thing technically: BEACON assesses PCF dataset quality before machine-learning modelling and uses explicit validation rules rather than only conventional cleaning. 


# 2. The easiest way to understand the whole project

Imagine we have this row:

| Product      | Country | Weight |         PCF | Year | Protocol |
| ------------ | ------- | -----: | ----------: | ---: | -------- |
| Steel bottle | UK      | 0.5 kg | 2.4 kg CO₂e | 2022 | ISO      |

A normal data-cleaning approach might ask:

> “Is anything missing?”

Maybe Pandas tells us:

```text
No missing values
```

So we say:

> Great! The data is clean.

**But is it actually good data?**

That's where the problem begins.


## Suppose another row says:

| Product      | Country | Weight |               PCF | Year | Protocol |
| ------------ | ------- | -----: | ----------------: | ---: | -------- |
| Steel bottle | UK      | 0.5 kg | 2,400,000 kg CO₂e | 2022 | —        |

There may be **no missing values**.

Pandas might happily accept the row.

But for a PCF prediction model, something is clearly suspicious.

So:

**Clean ≠ Quality.**

That's probably the single most important sentence your teammate needs to understand.

# 3. What traditional Pandas cleaning does

Traditional preprocessing is usually something like:

```python
df.isnull()
df.dropna()
df.fillna()
df.drop_duplicates()
df.astype()
```

These operations are useful.

**We are NOT saying they are bad.**

They answer questions such as:

* Is something missing?
* Are there duplicate rows?
* Is the data type correct?
* Can I convert this column?
* Can I remove an obviously problematic record?

But they don't automatically answer:

> Is the PCF value physically plausible?

> Is the reporting methodology documented?

> Is the country represented consistently?

> Is the product category meaningful?

> Is the data sufficiently representative?

> Can I understand where this number came from?

> Are different fields logically consistent with each other?

That's the gap BEACON is trying to address.

Your report explicitly contrasts traditional preprocessing with BEACON's structured multi-dimensional assessment. 

# 4. Then why do we need 8 dimensions?

This is where your teammate probably got confused.

Think of **data quality as a student taking eight different exams.**

One exam cannot tell you everything about the student.

For example:

### Exam 1 — Completeness

> Did the company provide the information?

Example:

```text
Product Weight = missing
```

Bad completeness.


### Exam 2 — Validity

> Is the value in an acceptable form/domain?

Example:

```text
Year = "banana"
```

Clearly invalid.

Or:

```text
Country = "UKKKKK"
```

Potentially invalid according to the accepted domain.


### Exam 3 — Consistency

> Does the information follow the expected representation and agree structurally?

Example:

```text
Country:
UK
United Kingdom
U.K.
United kingdom
```

These may refer to the same country but are represented inconsistently.


### Exam 4 — Plausibility

This is particularly important for your PCF project.

> Does the number make sense physically/business-wise?

Imagine:

```text
Product Weight = 0.5 kg
PCF = 50,000 kg CO₂e
```

It may technically be a number.

It may even pass a datatype check.

But it could be highly suspicious.

Your report specifically defines plausibility as assessing whether numerical values are physically realistic. 


### Exam 5 — Traceability

> Can we understand where the information came from?

For example:

```text
PCF = 2.4 kg CO₂e
Protocol = ISO 14067
Source = ...
```

versus:

```text
PCF = 2.4
Source = blank
Methodology = blank
```

The second record may contain a perfectly reasonable number, but we have less evidence about its origin.

This is especially relevant in sustainability reporting.


### Exam 6 — Timeliness

> Is the information temporally relevant?

For example:

```text
Reporting Year = 2022
```

A historical benchmark dataset may legitimately contain old data.

But in an ongoing reporting system, you may want to know whether records are sufficiently current.

Your report actually makes a sensible distinction here: the freshness rule was excluded from the static historical Carbon Catalogue because comparing historical records to today's date would not be meaningful. 

That's a **good methodological decision**, not a weakness.

### Exam 7 — Interpretability

> Can a human understand what the information means?

For example:

```text
Change Reason = "Updated"
```

versus:

```text
Change Reason = "Supplier emission factor updated"
```

The second is more interpretable.


### Exam 8 — Representativeness

> Does the dataset adequately cover the population we want to learn from?

Suppose your dataset has:

```text
95% electronics
5% everything else
```

The dataset might have:

* no missing values,
* valid data types,
* consistent values,
* plausible carbon values.

Yet it may still be poorly representative.

That's important for ML because a model learns from the distribution of its training data.

Your report defines representativeness in terms of dataset diversity and coverage. 

# 5. So why not just use one "data quality score"?

Because different problems mean different things.

Imagine two datasets:

### Dataset A

```text
Completeness = 95%
Validity = 95%
Consistency = 95%
Plausibility = 50%
Traceability = 90%
...
```

### Dataset B

```text
Completeness = 50%
Validity = 95%
Consistency = 95%
Plausibility = 95%
Traceability = 90%
...
```

Both could have an overall score around a similar level.

But **the problem is completely different**.

Dataset A has a plausibility problem.

Dataset B has a completeness problem.

That's why BEACON doesn't jump directly to one score.

It goes:

**Individual rules → dimensions → overall quality**

Your architecture explicitly follows this sequence. 


# 6. And this is where the Feature–Dimension Mapping becomes important

This is actually one of the strongest ideas in your framework.

You don't say:

> "Every column must be tested against all eight dimensions."

Instead, you ask:

> **Which quality dimensions actually make sense for this particular feature?**

For example:

### Product Weight

Relevant:

* Completeness
* Validity
* Consistency
* Plausibility

Not necessarily:

* Representativeness
* Timeliness

### Product Name

Relevant:

* Completeness
* Interpretability

Not necessarily:

* Plausibility

You wouldn't ask:

> "Is the product name physically plausible?"

That doesn't make sense.

Your report explicitly says BEACON applies dimensions selectively according to the semantic role of each feature rather than evaluating every feature against every dimension. 

**That is much better than randomly applying eight checks to every column.**


# 7. So did we randomly choose the eight dimensions?

### No.

And this is something your teammate should be able to say confidently.

The report says the dimensions were synthesised from:

* Wang & Strong
* ISO/IEC 25012
* ISO 8000
* DAMA UK
* ISO 14067
* GHG Protocol
* PCF-specific/domain literature

and then filtered using three criteria:

### 1. Measurability

Can we measure it?

### 2. Rule Definition

Can we define an actual validation rule?

### 3. Computability

Can a computer automatically evaluate it?

Your report explicitly documents these three criteria. 

So the logic is:

**Research literature → candidate dimensions → PCF requirements → measurable/rule-based/computable → eight selected dimensions**

That is very different from:

> "We thought eight dimensions sounded good."


# 8. Why are international standards important?

This is where BEACON gets much stronger.

You are not saying:

> "We invented data quality."

You're saying:

> "Established data-quality and carbon-accounting standards already identify important quality concepts. We adapted and operationalised those concepts for PCF machine-learning data."

For example, ISO/IEC 25012 is specifically a general data-quality model and says it can be used to define data-quality requirements, measures and evaluations. ([ISO][1])

ISO 8000 also explicitly addresses data quality principles and measurement, while ISO/TS 8000-82 specifically discusses creating data rules for assessing data. ([ISO][2])

And for the carbon side, ISO 14067 is an international standard covering principles, requirements and guidelines for quantifying and reporting product carbon footprints. ([ISO][3])

The GHG Protocol Product Standard similarly provides a methodology for understanding full life-cycle emissions of products. ([GHG Protocol][4])

So BEACON sits at the intersection:

```text
             DATA QUALITY
                  ↓
       ISO / Data Quality Literature
                  ↓
              BEACON
                  ↓
        PCF-specific interpretation
                  ↓
        Validation Rules
                  ↓
          ML-ready Dataset
```

That is the academic story.


# 9. Is BEACON "internationally acceptable"?

Here we need to be **very precise**.

Don't tell your teammate:

> ❌ "BEACON is internationally accepted."

That would be too strong.

BEACON is **your research framework**. It has not suddenly become an ISO standard or internationally certified framework.

Instead say:

> **"BEACON is designed using internationally recognised data-quality and carbon-accounting principles, but BEACON itself is a research framework that requires further external validation before it could be claimed as an internationally validated standard."**

That answer is academically much safer.

There is an important distinction:

### Internationally recognised foundations

Yes.

ISO/IEC 25012, ISO 8000, ISO 14067 and GHG Protocol are internationally recognised frameworks/standards. ([ISO][1])

### BEACON itself internationally accepted?

Not yet.

Because that would require things such as:

* independent validation,
* testing on other PCF datasets,
* replication by other researchers,
* comparison with alternative quality frameworks,
* potentially expert evaluation,
* evidence that BEACON quality scores relate to downstream ML performance.

And **this is actually an opportunity for your dissertation rather than something to hide.**


# 10. Is BEACON academically valid?

I'd answer:

### **Yes, it has a credible academic foundation — but the strength of the claim depends on validation.**

There are two parts.

## Part A — Construct/design validity

You have a logical chain:

```text
Literature
   ↓
Standards
   ↓
PCF domain requirements
   ↓
8 dimensions
   ↓
Feature categories
   ↓
Feature–Dimension Mapping
   ↓
Validation rules
   ↓
Quality scores
```

Your report documents exactly this architecture. 

That is academically defensible as a **framework design methodology**.


## Part B — Empirical validation

This is where you need evidence.

The really powerful question is:

> **Does BEACON actually make a difference to ML prediction?**

For example:

### Experiment 1

Train model using conventional preprocessing.

```text
Raw data
 ↓
Pandas cleaning
 ↓
ML model
 ↓
RMSE / MAE / R²
```

### Experiment 2

Use BEACON.

```text
Raw data
 ↓
BEACON assessment
 ↓
Quality classification
 ↓
Quality-controlled data
 ↓
ML model
 ↓
RMSE / MAE / R²
```

Then compare.

If BEACON improves:

* RMSE,
* MAE,
* R²,
* model stability,

then you have empirical evidence that the framework matters. And this connects directly to your dissertation research question.



# 11. The biggest misunderstanding: BEACON does NOT replace Pandas

This is extremely important.

Tell your teammate:

> **"Pandas cleans the data. BEACON judges the quality of the data."**

They're complementary.

For example:

### Pandas

```python
df.drop_duplicates()
df.fillna()
df.astype()
```

might repair or transform data.

### BEACON

asks:

```text
Why is the value missing?

Is the value valid?

Is it plausible?

Is it consistent?

Is its provenance available?

Is the information interpretable?

Is the dataset representative?
```

So:

```text
Traditional preprocessing
        ↓
Clean the dataset
```

whereas:

```text
BEACON
        ↓
Assess whether the dataset is trustworthy
        ↓
Identify where quality problems exist
        ↓
Quantify the problems
        ↓
Classify quality
```

# 12. A very simple example of why null handling isn't enough

Imagine:

```text
Product Weight = 1 kg
PCF = 3 kg CO₂e
```

No missing values.

Pandas:

> ✅ Fine.

Now:

```text
Product Weight = 1 kg
PCF = 30,000 kg CO₂e
```

No missing values.

Pandas:

> ✅ Fine.

But BEACON's **Plausibility** assessment asks whether that numerical value is realistic.

That's the difference.

---

# 13. Another example: missing values

Suppose:

```text
Protocol Used for PCF = NaN
```

Pandas can tell you:

```python
df["Protocol Used for PCF"].isna()
```

But then what?

You might:

```python
df["Protocol Used for PCF"].fillna("Unknown")
```

Now there are no nulls.

But did the **quality** improve?

Not necessarily.

You simply replaced:

```text
Unknown information
```

with:

```text
"Unknown"
```

The information is still unavailable.

BEACON's job is not to pretend the information exists.

It records the quality problem.

That's an important conceptual difference.

# 14. BEACON's scoring is useful because it creates evidence

Suppose your dataset gets:

| Dimension          | Score |
| ------------------ | ----: |
| Completeness       |   92% |
| Validity           |   96% |
| Consistency        |   88% |
| Plausibility       |   61% |
| Traceability       |   55% |
| Timeliness         |   90% |
| Interpretability   |   81% |
| Representativeness |   70% |

Now you can say:

> "The dataset is not simply clean or dirty. Its strongest weaknesses are traceability and plausibility."

That's much more informative than:

> "There are 37 missing values."


# 15. And then the 15 rules give evidence for the scores

The eight dimensions are **what we want to assess**.

The rules are **how we assess them**.

For example:

### Completeness

```text
R01 Missing Value Check
```

### Validity

```text
R02 Data Type Validation
R03 Domain Validation
```

### Consistency

```text
R04 Controlled Vocabulary
R05 Unit Consistency
R08 Identifier Uniqueness
```

### Plausibility

```text
R06 Range Validation
R07 Cross-Field Validation
```

and so on.

Your report documents 15 generic patterns, of which 14 were executed on the Carbon Catalogue and one was deliberately excluded because freshness was not meaningful for the static historical dataset. 

So the architecture is:

```text
DIMENSION
   ↓
"What type of quality?"

RULE
   ↓
"How do we measure it?"

SCORE
   ↓
"How good is it?"

OVERALL SCORE
   ↓
"How good is the dataset overall?"
```


# 16. Why 15 generic rules instead of hundreds of rules?

This is another clever part of your design.

Suppose you have 25 features.

You could manually write:

```text
Rule for Product Weight
Rule for Product Name
Rule for Country
Rule for Company
...
```

That becomes messy.

Instead you created **generic reusable rule patterns**.

For example:

```text
R02 = Data Type Validation
```

can operate on all features where data type validity is relevant.

Your report specifically explains that the generic rule functions are reused across applicable features rather than creating a separate rule object for every feature. 

That gives BEACON a more scalable structure.


# 17. The architecture is actually easy to explain visually

Tell your teammate to remember this:

```text
                 BEACON
                    │
                    ▼
             RAW PCF DATA
                    │
                    ▼
         ┌─────────────────────┐
         │ 1. Categorise data  │
         └─────────────────────┘
                    │
                    ▼
         ┌─────────────────────┐
         │ 2. Map features to  │
         │    quality dimensions│
         └─────────────────────┘
                    │
                    ▼
         ┌─────────────────────┐
         │ 3. Apply validation │
         │    rules            │
         └─────────────────────┘
                    │
                    ▼
         ┌─────────────────────┐
         │ 4. Calculate scores │
         └─────────────────────┘
                    │
                    ▼
       ┌──────────────────────────┐
       │ 8 Dimension Scores       │
       └──────────────────────────┘
                    │
                    ▼
       ┌──────────────────────────┐
       │ Overall BEACON Score     │
       └──────────────────────────┘
                    │
                    ▼
       ┌──────────────────────────┐
       │ Quality Classification   │
       └──────────────────────────┘
                    │
                    ▼
              ML MODELLING
```

This is BEACON.


# 18. The strongest answer to "Why BEACON?"

If someone asks your teammate:

> **"Why did you develop BEACON?"**

She can answer:

> **"Traditional preprocessing can identify and repair individual data problems such as missing values, duplicates and incorrect data types, but it does not provide a systematic assessment of whether PCF data is trustworthy for machine learning. BEACON was developed to address this gap by evaluating PCF data across multiple quality dimensions, using literature- and standard-informed validation rules, and producing interpretable quality scores before modelling."**

That's a strong academic answer.


# 19. If they ask "Why eight dimensions?"

Answer:

> **"We did not choose the eight dimensions arbitrarily. We reviewed established data-quality literature and international standards and then selected dimensions that were relevant to PCF data and could be measured, expressed as validation rules, and automated. The eight dimensions therefore represent a tailored synthesis rather than a random selection."**

That is directly supported by your methodology. 


# 20. If they ask "Why not just use Pandas?"

Answer:

> **"Pandas is a preprocessing tool, whereas BEACON is a quality-assessment framework. Pandas can identify or handle missing values, duplicates and data types, but BEACON evaluates broader properties such as plausibility, traceability, interpretability and representativeness. Therefore, BEACON complements conventional preprocessing rather than replacing it."**

This is probably the answer your teammate needs most.


# 21. If they ask "Did you invent these dimensions?"

Answer:

> **"No. The dimensions were synthesised from established data-quality literature, international standards and PCF-specific requirements. What we developed ourselves is the BEACON-specific integration: the feature categorisation, Feature–Dimension Mapping, rule patterns, validation engine and scoring mechanism."**

That distinction is **very important**.

You didn't invent the concept of:

> completeness

or

> validity

or

> consistency.

You developed a **PCF-specific operational framework that combines them and turns them into executable rules.**

# 22. If they ask "Is this internationally recognised?"

Don't overclaim.

Say:

> **"BEACON itself is not an internationally certified standard. However, its design is grounded in internationally recognised standards such as ISO/IEC 25012, ISO 8000, ISO 14067 and the GHG Protocol. Therefore, the framework has an internationally grounded methodological foundation, while broader international validation would require testing by independent researchers across multiple datasets and contexts."**

This is probably the **most academically mature answer**.

ISO/IEC 25012 is explicitly a data-quality model, while ISO 14067 addresses product carbon-footprint quantification and reporting. ([ISO][1]) The GHG Protocol Product Standard is also designed for product life-cycle emissions accounting and was developed through a broad multi-stakeholder process. ([GHG Protocol][4])


# 23. If someone says "Your scoring system is arbitrary"

This is one question I would prepare for.

They might ask:

> "Why should 90% mean high quality? Why average the dimensions?"

That is a legitimate methodological question.

Your current report explains **how** the scores are aggregated, but this is an area where you should be careful not to claim that the chosen aggregation is universally established.

Your answer should be:

> **"The BEACON score is an operational research metric designed to provide a consistent quantitative summary of the rule outcomes. It is not claimed to be a universal or internationally standardised quality score. The purpose is to enable systematic comparison of data quality and investigate whether quality differences are associated with differences in machine-learning performance."**

That is much stronger than pretending the score itself is an international standard.


# 24. And this connects directly to your dissertation

This is the beautiful part.

Your project isn't ultimately:

> "We created eight scores."

Your real research question is:

> **Does systematic data-quality assessment improve the reliability of machine-learning prediction?**

Therefore:

```text
BEACON
   ↓
Identify quality problems
   ↓
Quantify quality
   ↓
Separate/assess quality levels
   ↓
ML modelling
   ↓
Compare performance
```

Then your evidence comes from:

```text
              MODEL PERFORMANCE

Traditional preprocessing
          VS
BEACON-informed preprocessing
          ↓
      RMSE
      MAE
       R²
```

If the BEACON-informed approach performs better, you have evidence supporting the usefulness of systematic data-quality assessment.

If it doesn't improve performance, **that is still a research result**.

You should not design the experiment assuming BEACON must win.


# 25. One very important distinction for your team

I would teach your teammate these four words:

### **Cleaning**

> Change the data.

### **Validation**

> Check whether the data satisfies a rule.

### **Quality assessment**

> Measure how good/trustworthy the data is across multiple criteria.

### **Machine learning**

> Learn patterns from the data.

BEACON primarily sits here:

```text
Cleaning → Validation → QUALITY ASSESSMENT → ML
```

It can inform cleaning, but **it is not simply another cleaning script.**

# 26. The "8 dimensions" in one memorable sentence each

Have her memorise this:

| Dimension              | Easy meaning                                           |
| ---------------------- | ------------------------------------------------------ |
| **Completeness**       | Is the required information there?                     |
| **Validity**           | Is the information allowed/correct according to rules? |
| **Consistency**        | Is it represented consistently?                        |
| **Plausibility**       | Does the value make realistic sense?                   |
| **Traceability**       | Can we understand where it came from?                  |
| **Timeliness**         | Is the information temporally relevant?                |
| **Interpretability**   | Can we understand what it means?                       |
| **Representativeness** | Does the dataset adequately cover the population?      |

Then:

> **Eight dimensions = eight different ways of asking whether the data can be trusted.**

That's the easiest explanation.


# 27. And the whole BEACON story in 30 seconds

If she has only 30 seconds during a presentation, tell her to say:

> **"Our problem was that conventional data preprocessing mainly focuses on technical issues such as missing values, duplicates and data types. For PCF prediction, however, data quality is broader. A value can be complete and technically valid but still be implausible, poorly documented, inconsistent or unrepresentative. Therefore, we developed BEACON as a structured quality-assessment framework. We selected eight dimensions based on established data-quality literature, international standards and PCF-specific requirements. We then mapped relevant dataset features to these dimensions and converted the mappings into 15 reusable validation rule patterns. The rules produce dimension-level scores and an overall quality score, allowing us to assess data quality systematically before machine-learning modelling."**

That is your **core presentation answer**.

# 28. My honest assessment of BEACON

If I were reviewing the methodology, I would say:

### 🟢 Strong

**1. Literature/standards grounding**

You aren't choosing dimensions randomly.

**2. Clear architecture**

The chain:

> feature → dimension → rule → score

is logical.

**3. Domain-specific adaptation**

You're not blindly copying a generic data-quality framework. You're adapting it to PCF.

**4. Feature–Dimension Mapping**

This is one of the strongest conceptual parts because it prevents irrelevant quality tests.

**5. Rule-based implementation**

The framework is computational rather than purely conceptual.

**6. Reusability**

Generic rules make the framework easier to adapt.

**7. Explicit treatment of the freshness issue**

Excluding freshness for a static historical dataset is defensible and shows methodological reasoning rather than blindly executing every rule. 

### 🟡 Needs careful handling

**1. Eight dimensions need strong literature justification**

You have this, but make the sources and rationale very clear.

**2. The overall scoring method is a design choice**

Don't present it as an internationally standardised scoring formula.

**3. Thresholds/classification need justification**

If you say:

```text
80–100 = High
60–79 = Medium
<60 = Low
```

you need to explain where those thresholds come from.

**4. External validation**

Testing only one dataset limits generalisability.

**5. ML impact is crucial**

Your dissertation becomes much stronger if you demonstrate:

> conventional preprocessing vs BEACON-informed quality assessment.


# 29. The one sentence I want your teammate to remember

If she forgets everything else, tell her:

> ### **"BEACON does not ask only whether the data is clean; it asks whether the data is trustworthy, why it is trustworthy, where it is weak, and whether that quality matters for machine-learning prediction."**

That is **why BEACON exists**.

And importantly, you are not claiming that BEACON has already become an internationally accepted standard. You are claiming that **its design is grounded in internationally recognised standards and research, while its effectiveness and generalisability are things your empirical evaluation needs to demonstrate.** That distinction will actually make you sound **more academically credible**, not less.

[1]: https://www.iso.org/standard/35736.html?utm_source=chatgpt.com "ISO/IEC 25012:2008 - Software engineering — Software product Quality Requirements and Evaluation (SQuaRE) — Data quality model"
[2]: https://www.iso.org/standard/81745.html?utm_source=chatgpt.com "ISO 8000-1:2022 - Data quality — Part 1: Overview"
[3]: https://www.iso.org/standard/71206.html?utm_source=chatgpt.com "ISO 14067:2018 - Greenhouse gases — Carbon footprint of products"
[4]: https://ghgprotocol.org/product-standard?utm_source=chatgpt.com "Product Standard | GHG Protocol"
