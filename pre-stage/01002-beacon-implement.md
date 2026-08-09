Absolutely. I've saved these as the working research questions for your MSc dissertation, so when we move into the implementation phase I'll make sure every step aligns with them.

### Main Research Question

> **To what extent does data quality assurance improve the accuracy and reliability of machine learning models for predicting product carbon footprints?**

### Supporting Research Question 1

> **What data quality issues exist in the Carbon Catalogue dataset, and how can they be identified and addressed using the proposed BEACON framework?**

### Supporting Research Question 2

> **How do different machine learning models compare in predicting product carbon footprints using data processed through the proposed BEACON framework?**

### Supporting Research Question 3

> **Does applying the proposed BEACON framework significantly improve prediction performance compared with using the original dataset?**

---

## This also defines our implementation roadmap

We'll implement BEACON so that every stage answers one or more of these questions.

| BEACON Stage                               | Purpose                                                                          | Research Question    |
| ------------------------------------------ | -------------------------------------------------------------------------------- | -------------------- |
| **Stage 1: Data Understanding**            | Explore the Carbon Catalogue dataset                                             | Foundation           |
| **Stage 2: Data Quality Assessment**       | Detect missing values, inconsistencies, duplicates, outliers, etc.               | **SRQ1**             |
| **Stage 3: BEACON Data Quality Assurance** | Clean data, apply quality rules, compute quality metrics/score                   | **SRQ1**             |
| **Stage 4: Feature Engineering**           | Prepare features for prediction                                                  | Supports SRQ2 & SRQ3 |
| **Stage 5: Machine Learning**              | Train Linear Regression, Random Forest, XGBoost, ANN (and others if appropriate) | **SRQ2**             |
| **Stage 6: Performance Comparison**        | Compare original dataset vs BEACON-processed dataset                             | **SRQ3**             |
| **Stage 7: Conclusions**                   | Determine whether data quality improves prediction accuracy and reliability      | **Main RQ**          |

---

## One important principle

From now on, every piece of code we write should answer a research question.

For example:

* **Notebook 01:** Data Understanding → supports the project foundation.
* **Notebook 02:** Data Quality Assessment → answers **SRQ1**.
* **Notebook 03:** BEACON Framework Implementation → answers **SRQ1**.
* **Notebook 04:** Feature Engineering → prepares for **SRQ2**.
* **Notebook 05:** Model Training → answers **SRQ2**.
* **Notebook 06:** Original vs BEACON Comparison → answers **SRQ3**.
* **Results & Discussion:** Synthesize the findings to answer the **Main Research Question**.

That way, your implementation, results, and dissertation chapters all stay aligned.

I also suggest one rule for the rest of the project:

> **If a step does not help answer the Main Research Question or one of the SRQs, we won't include it.**

This will keep the project focused, avoid unnecessary work, and make it much easier to justify every experiment in your dissertation.
