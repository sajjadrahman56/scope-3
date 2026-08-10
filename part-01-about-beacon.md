# 🌱 The Story of BEACON

> **“Forget the report for a moment. Forget the eight dimensions, rules, Python, scores, everything. Let me tell you how we actually arrived at BEACON.”**

Imagine one day we decided:

### **“Let's build an ML model that predicts the carbon footprint of products.”**

Sounds simple.

We have a dataset.

We have products.

We have carbon footprints.

We have machine learning.

So we thought:

> **“Let's clean the dataset and train the model.”**

And at that point, we were basically where we started.

---

## 🚗 Then imagine we want to buy a used car

Suppose I tell you:

> “I found a second-hand car. It's cheap. Let's buy it.”

You ask me:

> “Is the car good?”

I say:

> “Yes! I checked it.”

You ask:

> “What did you check?”

I say:

> “The car has four wheels.”

😂

You would obviously say:

> **“That's not enough!”**

Having four wheels doesn't mean the car is trustworthy.

You would want to check:

* Does it start?
* Is the engine healthy?
* Has it been in an accident?
* Is the mileage believable?
* Are the documents available?
* Is the model/year correct?
* Is the information consistent?
* Is the seller's information trustworthy?

Now we suddenly understand the **BEACON idea**.


# 🧹 Data cleaning is like washing the car

Imagine we take the car to a mechanic.

He cleans it.

He removes dirt.

He fixes some scratches.

He checks whether a tyre is missing.

He changes some oil.

Then he says:

> **“The car is clean.”**

Would you immediately buy it?

### No.

Because:

> **Clean does not necessarily mean trustworthy.**

This is exactly the problem with traditional data preprocessing.

Pandas can help us:

* find missing values,
* remove duplicates,
* change data types,
* standardise values,
* clean columns.

That's useful.

But after cleaning, we still need to ask:

> **“Can we trust this data?”**

# 🔍 So we started asking better questions

We looked at our PCF dataset and realised:

A carbon value can exist...

but maybe it's unrealistic.

A company name can exist...

but maybe it's written differently in different records.

A product can have a carbon footprint...

but maybe we don't know where that number came from.

A dataset can have no missing values...

but maybe 90% of the records come from one type of industry.

A value can technically be valid...

but still not make physical sense.

And suddenly we realised:

> **“Wait. Data quality is much bigger than missing values.”**



# 💡 This was the moment BEACON was born

We asked:

> **“What does it actually mean for PCF data to be good?”**

We didn't invent the answer from our imagination.

We went to the research literature and standards.

We looked at established data-quality concepts and PCF/carbon-accounting requirements.

Then we asked:

> “Which quality characteristics actually matter for our PCF dataset?”

And we selected eight dimensions based on the three practical conditions:

**Can we measure it?**

**Can we define a rule for it?**

**Can a computer calculate it?**

That's documented in your report. 


# 🏥 Think of BEACON like a medical check-up

This is probably the **best analogy** for your teammate.

Imagine you go to a doctor.

The doctor doesn't say:

> “Your blood pressure is okay, therefore you are completely healthy.”

They check several things.

### Blood pressure

One aspect.

### Temperature

Another aspect.

### Blood test

Another.

### Heart

Another.

### Medical history

Another.

Each test tells us something different.

And finally the doctor says:

> **“Overall, this looks healthy, but there is one area we should investigate.”**


# 🧬 BEACON does the same thing to data

Instead of checking a human body:

**BEACON checks the health of the dataset.**

### Completeness asks:

> “Is the information there?”

### Validity asks:

> “Is the information acceptable?”

### Consistency asks:

> “Is the information represented consistently?”

### Plausibility asks:

> “Does the number actually make sense?”

### Traceability asks:

> “Can we understand where it came from?”

### Timeliness asks:

> “Is the information relevant to the reporting time?”

### Interpretability asks:

> “Can we understand what the information means?”

### Representativeness asks:

> “Does the dataset adequately represent what we want to model?”

Your report defines these eight purposes explicitly. 


# 🎯 Why eight?

Then she might ask:

> “But why eight? Why not five? Why not ten?”

The answer is:

> **Because we didn't start with the number eight.**

We started with the **quality problems that matter**.

The research literature and standards gave us candidate concepts.

Then we considered:

> “Does this matter for PCF?”

> “Can we measure it?”

> “Can we create a rule?”

> “Can Python evaluate it?”

After that process, we arrived at eight dimensions.

So:

**8 is the result.**

It wasn't:

**“We need eight dimensions, let's find eight.”**

That's an important difference.


# 🗂️ Then another problem appeared

We had 25 columns.

For example:

```text
Product Name
Company
Country
Product Weight
PCF
Carbon Intensity
Reporting Year
Protocol
Upstream CO2
Transport CO2
...
```

Then we asked:

> “Should we check every column for every dimension?”

No.

That would be silly.

For example:

### Product Weight

Plausibility makes sense.

### Product Name

Plausibility doesn't really make sense.

You don't ask:

> “Is the product name physically plausible?”

😂

So we created the **Feature–Dimension Mapping**.

In simple language:

> **“For each column, decide which quality questions actually make sense.”**

Your report describes this as the conceptual core of BEACON. 


# 🧩 Then we needed a way to actually check the answers

Now we had:

```text
Product Weight
      ↓
Completeness
Validity
Consistency
Plausibility
```

But how do we actually measure those?

We turn them into rules.

For example:

### Completeness

> Is Product Weight missing?

### Validity

> Is Product Weight numeric?

### Consistency

> Is the unit represented correctly?

### Plausibility

> Is the value within a realistic range?

And suddenly:

> **Dimension → Rule**

Your report describes 15 generic rule patterns such as missing-value checks, data-type validation, domain validation, range validation, cross-field validation, provenance verification and others. 



# 🤖 Now BEACON becomes a machine

At this point, imagine BEACON as a **quality inspector**.

We give it the raw dataset.

BEACON walks through it.

It asks:

> “Is this complete?”

> “Is this valid?”

> “Is this consistent?”

> “Is this plausible?”

> “Can we trace it?”

And so on.

Each rule produces evidence.

Then BEACON combines those results.


# 📊 And finally we get a health report

Instead of saying:

> “The dataset is clean.”

BEACON can say something more useful:

```text
Completeness       92%
Validity           96%
Consistency        87%
Plausibility       61%
Traceability       55%
Timeliness         90%
Interpretability   81%
Representativeness 70%
```

Now we know something important:

> **“Our biggest problems aren't missing values. The bigger concerns are plausibility and traceability.”**

That's much more informative.


# 🚨 And THIS is why BEACON matters for ML

Now imagine we skip BEACON.

We take the dataset.

We clean missing values.

We remove duplicates.

We encode categories.

We train XGBoost.

The model gives us:

```text
R² = 0.84
```

We celebrate.

🎉

But wait.

### What if some carbon values were unrealistic?

### What if some categories were inconsistent?

### What if some values had poor provenance?

### What if the dataset was badly represented?

Then the model may be learning from **poor-quality information**.

So the question becomes:

> **“Can we trust the model if we haven't assessed the quality of the data it learned from?”**

That's the research motivation behind BEACON.



# 🔄 So BEACON sits BEFORE ML

The story is now very simple:

```text
        RAW DATA
            ↓
     "Is this data okay?"
            ↓
          BEACON
            ↓
 ┌─────────────────────────┐
 │ Completeness            │
 │ Validity                │
 │ Consistency             │
 │ Plausibility            │
 │ Traceability            │
 │ Timeliness              │
 │ Interpretability        │
 │ Representativeness      │
 └─────────────────────────┘
            ↓
     QUALITY EVIDENCE
            ↓
      QUALITY SCORE
            ↓
      QUALITY GROUP
            ↓
       ML MODEL
            ↓
    PREDICTION RESULTS
```

That's BEACON.



# 🧠 And now she should understand the name

**BEACON = Business Emissions Assessment and Carbon Output Network**

Think of a beacon.

A beacon is something that **helps you navigate**.

You are travelling through a dataset.

There are good-quality areas and dangerous/problematic areas.

BEACON shines a light on them.

It tells you:

> **“This part of your data looks reliable.”**

> **“This part needs attention.”**

> **“This dataset has weaknesses here.”**

And then you can make a better decision about using it for ML.


# 🎓 Now imagine an examiner asks her:

### “What exactly is your contribution?”

She shouldn't panic.

She can tell the story:

> **“Our contribution is not inventing the individual data-quality concepts. Those already exist in established literature and standards. Our contribution is integrating them into a PCF-specific, rule-based framework. BEACON maps PCF features to relevant quality dimensions, operationalises those dimensions through reusable validation rules, and produces quantitative quality evidence that can be used before machine-learning modelling.”**

That's a very defensible answer.



# 🗣️ If she has to explain BEACON to a non-technical person

Tell her to forget all the terminology and say:

> **“Imagine you want to hire someone for an important job. You wouldn't only check whether their application form is complete. You would check whether their information is valid, whether their experience makes sense, whether their qualifications can be verified, whether the information is understandable, and whether their experience actually represents the job you need. BEACON does something similar, but instead of assessing a person, it assesses the quality of a Product Carbon Footprint dataset before we trust it with a machine-learning model.”**

If the person understands that analogy, they understand BEACON.



# ❤️ And one final thing for your teammate

I would tell her this directly:

> **“Don't be intimidated by the Chapter 3 terminology. The technical report makes BEACON look complicated because we had to describe every component academically. But the idea itself is simple. We wanted to know whether our PCF data was actually trustworthy before asking a machine-learning model to learn from it. We studied what data quality means, selected the relevant dimensions, connected those dimensions to the appropriate columns, converted them into rules, ran the rules, calculated quality scores, and then used that quality information before modelling. That's the whole story.”**

And honestly, **if she can explain that story without looking at the report, she understands BEACON.**

The tables, mappings, rule IDs, formulas and Python implementation are just the **technical machinery underneath that story**.
