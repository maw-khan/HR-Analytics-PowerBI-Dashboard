# DAX Measures & Analytical Calculations

## 📌 Overview

DAX (Data Analysis Expressions) was used in the HR Analytics Dashboard to create analytical calculations and KPIs from the employee-level `HR_Analytics` dataset.

The DAX layer supports analysis of:

* Workforce size
* Employee attrition
* Average income
* Employee age
* Employee tenure
* Job level
* Performance
* Job satisfaction
* Environment satisfaction
* Work-life balance
* Department-level comparisons

The purpose of the analytical layer is to convert employee-level records into reusable metrics that can respond dynamically to the filters and context applied within the Power BI report.

---

# 🧮 Core KPI Measures

## 1. Total Employees

The dashboard displays:

**Total Employees: 1.47K**

This KPI represents the number of employees included in the HR dataset.

Conceptually:

```DAX
Total Employees =
COUNTROWS(HR_Analytics)
```

> The exact implementation of the measure in the PBIX is not exposed in the PDF export. The formula above represents the underlying analytical logic rather than a verified copy of the original PBIX formula.

---

# 🚪 2. Attrition Rate

The dashboard reports:

**Attrition Rate: 16.1%**

Attrition rate measures the proportion of employees classified as having left the organization relative to the total employee population.

Conceptually:

```DAX
Attrition Rate =
DIVIDE(
    Attrition Employees,
    Total Employees,
    0
)
```

where:

```text
Attrition Employees
=
Employees where Attrition = "Yes"
```

The resulting measure is displayed as a percentage in the dashboard.

---

# 💰 3. Average Monthly Income

The dashboard reports:

**Average Monthly Income: 6.50K**

This KPI represents the average value of `MonthlyIncome` across the employee population.

Conceptually:

```DAX
Average Monthly Income =
AVERAGE(HR_Analytics[MonthlyIncome])
```

This measure is also used to support compensation analysis across departments.

---

# ⏳ 4. Average Tenure

The dashboard reports:

**Average Tenure: 7.01**

The metric represents average employee tenure based on the company's tenure field:

```text
YearsAtCompany
```

Conceptually:

```DAX
Average Tenure =
AVERAGE(HR_Analytics[YearsAtCompany])
```

This provides a high-level view of employee experience within the organization.

---

# 🎂 5. Average Age

The dashboard reports:

**Average Age: 37**

This KPI represents the average age of employees.

Conceptually:

```DAX
Average Age =
AVERAGE(HR_Analytics[Age])
```

The report also complements this KPI with an age-group distribution.

---

# 📊 6. Average Job Level

The dashboard reports:

**Average Job Level: 2**

The measure provides an aggregated view of the `JobLevel` field.

Conceptually:

```DAX
Average Job Level =
AVERAGE(HR_Analytics[JobLevel])
```

This is used as a high-level indicator of the workforce's organizational level distribution.

---

# ⭐ 7. Average Performance Rating

The dashboard reports:

**Average Performance Rating: 3.15**

Performance is represented through the `PerformanceRating` field.

Conceptually:

```DAX
Average Performance Rating =
AVERAGE(HR_Analytics[PerformanceRating])
```

The same analytical metric is evaluated under department filter context to produce departmental performance comparisons.

---

# 😊 8. Average Job Satisfaction

The dashboard reports:

**Average Job Satisfaction: 2.68**

Conceptually:

```DAX
Average Job Satisfaction =
AVERAGE(HR_Analytics[JobSatisfaction])
```

The measure can be evaluated across departments to compare employee job satisfaction.

---

# 🏢 9. Average Environment Satisfaction

The dashboard reports:

**Average Environment Satisfaction: 2.72**

Conceptually:

```DAX
Average Environment Satisfaction =
AVERAGE(HR_Analytics[EnvironmentSatisfaction])
```

This measure supports analysis of employee satisfaction with the workplace environment.

---

# ⚖️ 10. Average Work-Life Balance

The dashboard reports:

**Average Work-Life Balance: 2.76**

Conceptually:

```DAX
Average Work-Life Balance =
AVERAGE(HR_Analytics[WorkLifeBalance])
```

The measure is also evaluated by department in the Performance section.

---

# 🔍 Filter Context & Department Analysis

One of the important analytical concepts demonstrated by the dashboard is **filter context**.

A measure such as:

```DAX
Average Job Satisfaction =
AVERAGE(HR_Analytics[JobSatisfaction])
```

does not necessarily return one fixed value.

When `Department` is placed on a visual axis or used as a filter, Power BI evaluates the measure separately within each department's filter context.

Conceptually:

```text
                 Average Job Satisfaction
                            │
              ┌─────────────┼─────────────┐
              ▼             ▼             ▼
          R&D            Sales           HR
           2.73           2.75          2.60
```

The dashboard uses this behavior to compare employee experience across departments.

---

# 🏢 Department-Level Performance

The report evaluates performance using department as an analytical dimension.

Displayed average performance ratings are:

| Department             | Average Performance Rating |
| ---------------------- | -------------------------: |
| Research & Development |                       3.16 |
| Human Resources        |                       3.14 |
| Sales                  |                       3.14 |

This demonstrates how the same measure can produce different results when evaluated under different filter contexts.

---

# 😊 Department-Level Employee Experience

The dashboard compares three employee-experience measures across departments.

| Department             | Job Satisfaction | Environment Satisfaction | Work-Life Balance |
| ---------------------- | ---------------: | -----------------------: | ----------------: |
| Research & Development |             2.73 |                     2.74 |              2.73 |
| Sales                  |             2.75 |                     2.68 |              2.82 |
| Human Resources        |             2.60 |                     2.68 |              2.92 |

These values are generated by evaluating the relevant satisfaction measures within each department's context.

---

# 📊 Aggregation Strategy

Because the underlying dataset is employee-level, the choice of aggregation is important.

### Count-based analysis

Used for:

* Employee counts
* Employees by department
* Employees by age group
* Employees by job role
* Employees by salary slab
* Employees by education field

### Average-based analysis

Used for:

* Age
* Monthly income
* Tenure
* Job level
* Performance rating
* Job satisfaction
* Environment satisfaction
* Work-life balance

### Percentage-based analysis

Used for:

* Attrition rate
* Workforce distribution percentages

---

# 🧠 DAX Concepts Demonstrated

The project provides practical experience with several core DAX concepts.

## Aggregation Functions

Examples include:

```DAX
COUNTROWS()
AVERAGE()
```

These functions transform employee-level records into summary KPIs.

---

## Filter Context

Measures are evaluated according to the filters applied by:

* Departments
* Categories
* Visual axes
* Report/page filters
* Other interactive selections

For example:

```text
No Department Filter
        ↓
All Employees
        ↓
Overall KPI

Department = Sales
        ↓
Sales Employees
        ↓
Sales-specific KPI
```

---

## DIVIDE

Percentage calculations can use `DIVIDE()` rather than direct division to safely handle cases where the denominator may be zero.

Conceptually:

```DAX
DIVIDE(
    Numerator,
    Denominator,
    0
)
```

---

# 📈 Visual-Level Analytical Logic

The dashboard combines DAX measures with categorical fields to generate comparative visuals.

Examples include:

```text
Department
     +
Average Performance Rating
     ↓
Performance by Department
```

```text
Department
     +
Average Job Satisfaction
     ↓
Job Satisfaction by Department
```

```text
Department
     +
Average Monthly Income
     ↓
Monthly Income by Department
```

This approach allows reusable measures to drive multiple visualizations.

---

# 📌 KPI Summary

The completed dashboard presents the following high-level analytical metrics:

| Measure                          | Dashboard Result |
| -------------------------------- | ---------------: |
| Total Employees                  |            1.47K |
| Attrition Rate                   |            16.1% |
| Average Monthly Income           |            6.50K |
| Average Tenure                   |             7.01 |
| Average Age                      |               37 |
| Average Job Level                |                2 |
| Average Performance Rating       |             3.15 |
| Average Work-Life Balance        |             2.76 |
| Average Environment Satisfaction |             2.72 |
| Average Job Satisfaction         |             2.68 |

---

# 🎯 Why the DAX Layer Matters

The dashboard is not simply a collection of visualizations.

The analytical layer allows employee-level data to be converted into reusable business metrics that can be evaluated across different workforce segments.

The workflow can be represented as:

```text
Employee Records
       ↓
DAX Measures
       ↓
Filter Context
       ↓
Aggregated KPIs
       ↓
Comparative Visualizations
       ↓
HR Insights
```

This makes the dashboard interactive and analytical rather than purely descriptive.

---

# ⚠️ Formula Verification Note

The PDF export provides the final KPI values and visual outputs but does not expose the underlying DAX definitions stored inside the `.pbix` file.

Therefore, formulas in this document are presented as **conceptual implementations of the calculations represented by the dashboard**, not as a claim that each formula is an exact transcription of the original PBIX measure.

Where exact PBIX measure definitions become available, this documentation can be updated to reflect the original implementations precisely.

---

# ✅ Summary

The DAX layer transforms the employee-level `HR_Analytics` dataset into reusable workforce metrics.

The resulting analytical measures support:

**Workforce Size → Attrition → Compensation → Demographics → Performance → Satisfaction → Work-Life Balance**

These calculations form the analytical foundation of the HR Analytics Power BI Dashboard.
