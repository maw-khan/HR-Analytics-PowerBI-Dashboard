# Data Model

## 📌 Overview

The HR Analytics Dashboard uses an employee-level analytical data structure centered around a single primary table:

```text
HR_Analytics
```

The table contains employee demographic, employment, compensation, attrition, satisfaction, performance, and tenure-related attributes.

Because the available dataset is already structured at the employee level, the dashboard does not require the multi-table transactional model used in projects such as hospital billing or appointment analytics.

---

# 🗃️ Primary Analytical Table

## `HR_Analytics`

The `HR_Analytics` table represents the core employee dataset used throughout the Power BI report.

Each row corresponds to an employee record.

The table contains **38 fields** covering several HR analytical dimensions.

### Employee Identifiers

| Field            | Purpose                    |
| ---------------- | -------------------------- |
| `EmpID`          | Employee identifier        |
| `EmployeeNumber` | Employee record identifier |
| `EmployeeCount`  | Employee count field       |

---

# 👥 Demographic Attributes

| Field            | Analytical Purpose                |
| ---------------- | --------------------------------- |
| `Age`            | Employee age                      |
| `AgeGroup`       | Employee age segmentation         |
| `Gender`         | Gender distribution               |
| `MaritalStatus`  | Marital-status analysis           |
| `Education`      | Education level                   |
| `EducationField` | Employee education specialization |

These fields support demographic analysis such as:

* Employee count by age group
* Gender distribution
* Education field distribution
* Marital status distribution
* Average employee age

---

# 🏢 Organizational Attributes

| Field                | Analytical Purpose          |
| -------------------- | --------------------------- |
| `Department`         | Department-level analysis   |
| `JobRole`            | Job-role distribution       |
| `JobLevel`           | Employee job level          |
| `BusinessTravel`     | Business-travel category    |
| `OverTime`           | Overtime status             |
| `NumCompaniesWorked` | Previous-company experience |

These fields allow the workforce to be segmented according to organizational structure and employment characteristics.

---

# 💰 Compensation Attributes

| Field               | Analytical Purpose                |
| ------------------- | --------------------------------- |
| `DailyRate`         | Daily compensation-related value  |
| `HourlyRate`        | Hourly compensation-related value |
| `MonthlyIncome`     | Monthly employee income           |
| `MonthlyRate`       | Monthly rate                      |
| `SalarySlab`        | Salary-range segmentation         |
| `PercentSalaryHike` | Salary increase percentage        |
| `StockOptionLevel`  | Stock-option level                |

These fields support:

* Average monthly income
* Salary slab distribution
* Department-level income analysis
* Compensation segmentation

---

# 📈 Performance & Satisfaction Attributes

The model contains several employee-experience and performance indicators.

| Field                      | Purpose                            |
| -------------------------- | ---------------------------------- |
| `PerformanceRating`        | Employee performance rating        |
| `JobSatisfaction`          | Job satisfaction rating            |
| `EnvironmentSatisfaction`  | Workplace environment satisfaction |
| `RelationshipSatisfaction` | Relationship satisfaction          |
| `WorkLifeBalance`          | Work-life balance rating           |
| `JobInvolvement`           | Employee job involvement           |

These fields are particularly important in the **Performance** section of the dashboard.

---

# ⏳ Experience & Tenure Attributes

| Field                     | Purpose                       |
| ------------------------- | ----------------------------- |
| `TotalWorkingYears`       | Total professional experience |
| `YearsAtCompany`          | Years spent at the company    |
| `YearsInCurrentRole`      | Years in current role         |
| `YearsSinceLastPromotion` | Time since last promotion     |
| `YearsWithCurrManager`    | Years with current manager    |
| `TrainingTimesLastYear`   | Training participation        |

These fields provide additional context for workforce and employee-experience analysis.

---

# 🚪 Attrition

The model includes:

```text
Attrition
```

This categorical field is used as the basis for the dashboard's attrition analysis.

The report presents:

* Overall attrition rate
* Attrition by department

This makes attrition one of the primary workforce KPIs in the report.

---

# 🧩 Model Structure

The conceptual structure of the model is:

```text
                         HR_Analytics
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
        ▼                     ▼                     ▼
   Demographics          Employment           Compensation
        │                     │                     │
   ┌────┼────┐          ┌─────┼─────┐         ┌────┼────┐
   │    │    │          │     │     │         │    │    │
  Age Gender Education  Dept JobRole JobLevel Income Salary Overtime
        │                     │                     │
        └─────────────────────┼─────────────────────┘
                              │
              ┌───────────────┼────────────────┐
              │               │                │
              ▼               ▼                ▼
          Attrition       Performance      Satisfaction
                              │                │
                              │       ┌────────┼─────────┐
                              │       │        │         │
                              │     Job Sat. Environment Work-Life
                              │                Sat.      Balance
                              │
                              ▼
                       Power BI Measures
                              │
                              ▼
                     Interactive Dashboard
```

---

# 📊 Analytical Relationships

Since the project is based on a single employee-level analytical table, there are no separate fact-to-dimension relationships required for the primary dashboard analysis.

Instead, analytical dimensions are represented as fields within `HR_Analytics`.

For example:

```text
HR_Analytics
     │
     ├── Department
     ├── JobRole
     ├── AgeGroup
     ├── Gender
     ├── SalarySlab
     ├── EducationField
     ├── Attrition
     ├── PerformanceRating
     ├── JobSatisfaction
     ├── EnvironmentSatisfaction
     └── WorkLifeBalance
```

Power BI measures and visual-level aggregations operate over these fields to generate the dashboard's KPIs and comparisons.

---

# 🧮 Analytical Layer

The data model acts as the foundation for the DAX layer.

Measures can evaluate the employee dataset according to the current filter context.

For example:

```text
Department
      ↓
Filter Context
      ↓
HR_Analytics
      ↓
DAX Measure
      ↓
Department-specific KPI
```

This allows the same analytical measures to be reused across different dashboard visuals.

---

# 🎯 Dashboard-to-Model Mapping

| Dashboard Area           | Main Model Fields                             |
| ------------------------ | --------------------------------------------- |
| Employee Overview        | Employee count, Age, Gender, Attrition        |
| Workforce                | Department, AgeGroup, EducationField, JobRole |
| Compensation             | MonthlyIncome, SalarySlab, Department         |
| Attrition                | Attrition, Department                         |
| Performance              | PerformanceRating, Department                 |
| Job Satisfaction         | JobSatisfaction, Department                   |
| Environment Satisfaction | EnvironmentSatisfaction, Department           |
| Work-Life Balance        | WorkLifeBalance, Department                   |
| Demographics             | Age, Gender, MaritalStatus, Education         |
| Tenure                   | YearsAtCompany, TotalWorkingYears             |

---

# 📌 Model Design Rationale

The single-table structure is appropriate for this particular dataset because the source data is already organized at the employee level and the dashboard primarily performs descriptive and comparative workforce analysis.

Keeping the employee records within one analytical table allows the report to directly segment and aggregate the workforce across:

**Demographics → Employment → Compensation → Attrition → Performance → Employee Experience**

without introducing unnecessary model complexity.

---

# 🔍 Key Modeling Considerations

### Employee-Level Grain

The fundamental grain of the dataset is the employee record.

Therefore, employee-level fields should generally be analyzed using appropriate aggregations rather than treating every numeric column as an additive business metric.

For example:

* Employee counts → Count/Distinct Count
* Monthly income → Average/Sum depending on analytical purpose
* Age → Average
* Performance rating → Average
* Satisfaction ratings → Average
* Tenure → Average

---

### Categorical Rating Fields

Several fields represent categorical rating scales rather than continuous financial or operational quantities.

Examples include:

* `JobSatisfaction`
* `EnvironmentSatisfaction`
* `RelationshipSatisfaction`
* `WorkLifeBalance`
* `PerformanceRating`
* `JobInvolvement`

The dashboard uses these fields primarily for category analysis and average rating comparisons.

---

# 📈 Dashboard Output

The model supports three main report sections:

```text
HR_Analytics
     │
     ├── Overview
     │      ├── Workforce KPIs
     │      ├── Attrition
     │      ├── Demographics
     │      └── Department Analysis
     │
     ├── Workforce
     │      ├── Education
     │      ├── Salary
     │      ├── Job Roles
     │      └── Demographics
     │
     └── Performance
            ├── Performance Rating
            ├── Job Satisfaction
            ├── Environment Satisfaction
            └── Work-Life Balance
```

---

# ✅ Summary

The Power BI data model is centered on the `HR_Analytics` employee-level table.

The model provides the foundation for analyzing:

* Workforce composition
* Employee attrition
* Department distribution
* Job roles
* Compensation
* Demographics
* Employee satisfaction
* Performance
* Work-life balance
* Employee tenure

The resulting model is intentionally straightforward, allowing the dashboard's analytical and visualization layers to remain focused on workforce insights rather than unnecessary data-model complexity.
