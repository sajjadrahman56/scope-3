# What can I extract from Microsoft's report?

For one company (Microsoft), I can create a row like this:

| Feature              | Available?        | Example                        |
| -------------------- | ----------------- | ------------------------------ |
| Company              | ✅                 | Microsoft                      |
| Year                 | ✅                 | 2024 (reported in 2025 report) |
| Industry             | ✅                 | Technology                     |
| Scope 1              | ✅                 | Yes                            |
| Scope 2              | ✅                 | Yes                            |
| Total Scope 3        | ✅                 | Yes                            |
| Scope 3 Category 1   | ✅                 | Purchased Goods & Services     |
| Scope 3 Category 2   | ✅                 | Capital Goods                  |
| Scope 3 Category 3   | ✅                 | Fuel & Energy                  |
| Business Travel      | ✅                 | Category 6                     |
| Employee Commuting   | ✅                 | Category 7                     |
| Waste                | ✅                 | Category 5                     |
| Downstream Transport | ✅                 | Category 9                     |
| Use of Sold Products | ✅                 | Category 11                    |
| Revenue              | ✅ (Annual Report) | Available                      |
| Employees            | ✅ (Annual Report) | Available                      |

---

# This is the important page

Look at **Page 13**.

Microsoft reports the breakdown of Scope 3 emissions by category. 

It says approximately:

| Scope 3 Category           | % of Scope 3 |
| -------------------------- | -----------: |
| Purchased Goods & Services |       34.04% |
| Capital Goods              |       40.83% |
| Fuel & Energy              |        4.40% |
| Upstream Transport         |        2.69% |
| Waste                      |        0.05% |
| Business Travel            |        1.70% |
| Employee Commuting         |        1.40% |
| Downstream Transport       |        0.29% |
| Use of Sold Products       |       11.83% |

This is **excellent research data**. 

---

# But here is the limitation

Notice what Microsoft **doesn't** tell you.

It **doesn't** say:

| Activity             | Value |
| -------------------- | ----- |
| Steel purchased      | ❌     |
| Concrete purchased   | ❌     |
| Plastic purchased    | ❌     |
| Truck km             | ❌     |
| Ship km              | ❌     |
| Supplier electricity | ❌     |

Therefore,

you **cannot** independently calculate

> Activity × Emission Factor

because the activity values are not disclosed.

---

# So what dataset can we build?

Actually, a very good one.

Imagine collecting reports from 100 companies.

Then your dataset becomes:

| Company   | Industry | Revenue | Employees | Scope1 | Scope2 | Total Scope3 | Cat1 | Cat2 | Cat3 | Cat5 | Cat6 | Cat7 | Cat11 |
| --------- | -------- | ------- | --------- | ------ | ------ | ------------ | ---- | ---- | ---- | ---- | ---- | ---- | ----- |
| Microsoft | Tech     | ...     | ...       | ...    | ...    | ...          | ...  | ...  | ...  | ...  | ...  | ...  | ...   |
| Apple     | Tech     | ...     | ...       | ...    | ...    | ...          | ...  | ...  | ...  | ...  | ...  | ...  | ...   |
| Shell     | Energy   | ...     | ...       | ...    | ...    | ...          | ...  | ...  | ...  | ...  | ...  | ...  | ...   |

This is a **real ESG dataset**.

---

# Now the big question...

Can this dataset calculate Scope 3?

## NO.

Because Scope 3 is **already reported**.

---

# Can this dataset train ML?

## YES.

For example,

Suppose Apple **doesn't report Business Travel**.

Microsoft does.

Google does.

Amazon does.

Your ML model predicts

Business Travel emissions.

Or

Suppose a company reports

Scope 1

Scope 2

Revenue

Employees

Industry

but

not Scope 3.

ML predicts Scope 3.

---

# This is the key insight

Originally we were thinking

> Collect reports → Calculate Scope 3

After reading Microsoft's report, I think the better workflow is

> Collect reports → Build ESG dataset → Simulate missing Scope 3 or missing categories → Train ML to estimate them.

---

# My concern

I **don't** think this alone is enough for a high-quality MSc dissertation.

Why?

Because if every company reports Scope 3, then we're simply hiding values artificially and asking ML to recover them. That's a valid machine learning experiment, but the research contribution may be limited unless it's tied to a real reporting problem.

---

# I have a better idea after reading the report

Remember your paper said:

> Companies often cannot report Scope 3 because supplier data are incomplete or unavailable. 

That suggests a stronger research question:

> **Can machine learning estimate missing Scope 3 categories (such as Purchased Goods & Services or Business Travel) using the remaining disclosed company information?**

That is much closer to the real-world problem than predicting an already reported total Scope 3 value.

## My recommendation

I think we should **stop downloading more reports for now**.

Instead, let's spend tomorrow answering one question:

> **Exactly what should the AI predict?**

Once we define that target, I can tell you **precisely** what data we need, whether Microsoft reports are sufficient, or whether we need additional datasets like CDP, EXIOBASE, or procurement data.

I genuinely think **this decision will determine whether your dissertation becomes average or genuinely strong**, so it's worth getting right before collecting hundreds of PDFs.
