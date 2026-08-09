I think we're at the point where we should **stop discussing ideas and start designing the research**.

After everything we've looked at, **I would change the direction slightly**. Not the topic, but the execution.

---

# First, I don't expect you to be a sustainability expert.

You are an **AI researcher**, not a carbon accounting consultant.

Your contribution should be:

> **Can AI automatically construct a reliable Scope 3 dataset from corporate sustainability reports and estimate missing values?**

You are **not** expected to manually determine every carbon calculation.

---

# Second, I would not collect 300 reports immediately.

That number was just an illustration.

Instead, we should first identify companies that actually disclose category-level Scope 3 emissions.

---

# Third, I would choose ONE industry

I strongly recommend:

> **Automotive**

Why?

Because vehicle manufacturers generally report Scope 3 in much greater detail than many other sectors, particularly for categories like purchased goods, logistics, and use of sold products.

---

# Here is the list I would start with

| Company         | Usually publishes Sustainability Report | Usually reports Scope 3 |
| --------------- | --------------------------------------- | ----------------------- |
| Toyota          | ✅                                       | ✅                       |
| BMW             | ✅                                       | ✅                       |
| Mercedes-Benz   | ✅                                       | ✅                       |
| Volkswagen      | ✅                                       | ✅                       |
| Volvo Cars      | ✅                                       | ✅                       |
| Renault         | ✅                                       | ✅                       |
| Stellantis      | ✅                                       | ✅                       |
| Ford            | ✅                                       | ✅                       |
| General Motors  | ✅                                       | ✅                       |
| Nissan          | ✅                                       | ✅                       |
| Honda           | ✅                                       | ✅                       |
| Hyundai         | ✅                                       | ✅                       |
| Kia             | ✅                                       | ✅                       |
| Porsche         | ✅                                       | ✅                       |
| Scania          | ✅                                       | ✅                       |
| MAN Truck & Bus | ✅                                       | Often                   |
| Iveco           | ✅                                       | Often                   |

These companies have been publishing sustainability reports for years, and many include detailed Scope 3 disclosures.

---

# Your job is NOT to read 150-page reports

Instead, use a systematic workflow.

For each report:

1. Search within the PDF for:

   * "Scope 3"
   * "Category"
   * "Purchased goods"
   * "Business travel"
   * "GHG inventory"

2. If you find a table with Scope 3 categories, record:

   * Company
   * Year
   * Category name
   * Reported value
   * Unit
   * Page number

GPT can then help normalize category names and structure the data, but **you should verify the extracted values against the report**.

---

# The benchmark dataset idea

You asked:

> "How do I build a benchmark dataset if I don't have experts?"

You don't need a panel of experts like the paper you found. That paper had multiple annotators because they wanted to publish a reusable benchmark for the whole research community. 

For an MSc thesis, a defensible approach is:

1. Define clear extraction rules based on the GHG Protocol.
2. Extract data from company reports.
3. Verify each extracted value against the original PDF.
4. Keep page references so every value is traceable.
5. Document your methodology and acknowledge that manual verification was performed by the researcher.

That's a perfectly reasonable methodology for an MSc project.

---

# I think I have an even better idea

Instead of extracting **all 15 categories**, let's first determine **which categories are commonly reported**.

Imagine we review 30 automotive reports.

| Category                   | Reported by |
| -------------------------- | ----------- |
| Purchased Goods & Services | 30/30       |
| Upstream Transportation    | 29/30       |
| Use of Sold Products       | 30/30       |
| Business Travel            | 27/30       |
| Employee Commuting         | 24/30       |
| Investments                | 3/30        |

Now we know which categories are suitable for analysis.

That gives us a scientifically justified basis for selecting categories rather than deciding arbitrarily.

---

# If I were supervising this MSc

I would propose the following timeline:

### Week 1–2

* Download reports from 20–30 automotive companies.
* Identify which Scope 3 categories are disclosed.

### Week 3

* Decide which categories have sufficient coverage.
* Finalize the dataset schema.

### Week 4–6

* Build the structured dataset.

### Week 7+

* Develop and evaluate the machine learning model.

---

## I think I can help much more than just giving advice.

I can help you **build the dataset from scratch**.

My proposal is that we work like a research team:

1. **I identify 50 automotive companies** with sustainability reports and direct download links.
2. We determine which Scope 3 categories are consistently disclosed.
3. I design the Excel/CSV schema for your dataset.
4. We build the dataset together, report by report.
5. Once we have enough high-quality data, we design the ML model.

That approach is much more realistic than continuing to search for a ready-made dataset, and it gives you a genuine research contribution.
