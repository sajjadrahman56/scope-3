This paper actually answers your question better than you might realize.

## The authors did **not** randomly search for Scope 3 reports.

They created **selection criteria**.

Look at what they wrote.

### Step 1 — They started with 29 automotive manufacturers

They first collected reports from **29 global automotive OEMs** (Original Equipment Manufacturers). 

Then they **filtered** them.

---

## Step 2 — They only kept companies that met these conditions

This is the important part.

The paper says the company **must**:

1. **Report Scope 1, Scope 2 and Scope 3 emissions**
2. **Report at least 10 of the 15 Scope 3 categories separately**
3. **Report Scope 3 Category 11 (Use of Sold Products)** because it is the most important category for automotive companies.
4. Report emissions in understandable units (e.g., tonnes CO₂e). 

After applying these rules,

they reduced

**29 companies → 13 companies**

because only 13 had sufficiently transparent reporting. 

---

# This is the breakthrough.

You asked me:

> **"How do I know which companies disclose detailed Scope 3?"**

This paper already tells us.

They have already identified **13 automotive companies** that disclose **at least 10 Scope 3 categories**.

That is exactly the type of dataset we need.

---

# Even better...

The paper lists the companies they used.

From the references and sampling section, they include companies such as:

* BMW
* Ford
* General Motors
* Hyundai
* Mazda
* Mercedes-Benz
* Mitsubishi
* Nissan
* Stellantis
* Subaru
* Toyota
* Volkswagen
* Volvo Cars 

These are not guesses—they are the companies that passed the paper's reporting-quality criteria.

---

# This changes our research completely.

Originally we were asking:

> Which companies disclose Scope 3?

Now we know.

Instead of searching the whole internet,

we start with these **13 companies**.

---

# Even better...

Look what they analyzed.

They examined all 15 Scope 3 categories.

For example:

* Category 1
* Category 2
* Category 3
* ...
* Category 15

They even counted how many companies reported each category. 

For example:

| Category            | Companies reporting |   |
| ------------------- | ------------------: | - |
| Scope 3 Category 1  |           **13/13** |   |
| Scope 3 Category 11 |           **13/13** |   |
| Category 2          |                9/13 |   |
| Category 3          |                9/13 |   |
| Category 5          |               10/13 |   |
| Category 6          |               13/13 |   |
| Category 7          |               12/13 |   |
| Category 8          |                3/13 |   |
| Category 10         |                5/13 |   |
| Category 13         |                7/13 |   |
| Category 14         |                6/13 |   |
| Category 15         |                4/13 |   |

---

# This is exactly what I wanted to know!

Notice something amazing.

Category 1 is reported by **every company**.

Category 11 is reported by **every company**.

Category 6 is reported by **every company**.

Category 7 is reported by **12 companies**.

So...

**You don't need all 15 categories.**

Your thesis can focus on the categories with sufficient reporting.

---

# If I were your supervisor today...

I would officially change your project.

Instead of

> Estimate missing values for all 15 Scope 3 categories.

I would write

> **Develop a machine learning framework for estimating missing values of commonly disclosed Scope 3 emission categories in the automotive industry.**

That is:

* much easier,
* scientifically justified,
* directly supported by this paper,
* and based on publicly available sustainability reports.

## My proposal

I think we now have a concrete and feasible path:

1. Use **these 13 automotive companies** as your initial dataset.
2. Download their sustainability reports for multiple years (e.g., 2020–2024).
3. Extract the categories that are consistently disclosed—especially Categories **1, 6, 7, and 11**.
4. Build your standardized dataset.
5. Then develop and evaluate your machine learning model for estimating missing values.

This is the first time in our discussions that I feel we have a **defensible MSc research methodology**, grounded in published literature rather than assumptions.
