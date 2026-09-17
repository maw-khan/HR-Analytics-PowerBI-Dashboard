# Data Preparation & Transformation

## 📌 Overview

The HR Analytics Dashboard is built from employee-level Human Resources data containing demographic, organizational, compensation, performance, satisfaction, and tenure-related attributes.

Before developing the dashboard, the dataset was prepared in Power BI to ensure that the fields could be used consistently for analysis and visualization.

The data preparation stage focused on making the employee dataset suitable for:

* Workforce analysis
* Attrition analysis
* Department comparisons
* Compensation analysis
* Job-role analysis
* Employee satisfaction analysis
* Performance analysis
* Dashboard-level KPI calculations

---

# 📥 Source Dataset

The source dataset contains employee-level records with attributes covering:

### Employee Information

* `EmpID`
* `EmployeeNumber`
* `EmployeeCount`
* `Over18`
* `StandardHours`

### Demographics

* `Age`
* `AgeGroup`
* `Gender`
* `MaritalStatus`
* `Education`
* `EducationField`

### Employment Information

* `Department`
* `JobRole`
* `JobLevel`
* `BusinessTravel`
* `OverTime`
* `NumCompaniesWorked`

### Compensation

* `DailyRate`
* `HourlyRate`
* `MonthlyIncome`
* `MonthlyRate`
* `PercentSalaryHike`
* `SalarySlab`
* `StockOptionLevel`

### Satisfaction & Engagement

* `EnvironmentSatisfaction`
* `JobInvolvement`
* `JobSatisfaction`
* `RelationshipSatisfaction`
* `WorkLifeBalance`

### Performance

* `PerformanceRating`

### Experience & Tenure

* `TotalWorkingYears`
* `YearsAtCompany`
* `YearsInCurrentRole`
* `YearsSinceLastPromotion`
* `YearsWithCurrManager`

### Attrition

* `Attrition`

---

# 🧹 Data Preparation Workflow

The overall preparation workflow can be represented as:

```text
Raw Employee Dataset
        │
        ▼
Data Import
        │
        ▼
Data Type & Field Preparation
        │
        ▼
Analytical Field Organization
        │
        ▼
Power BI Data Model
        │
        ▼
DAX Measures
        │
        ▼
Dashboard Visualizations
```

---

# 🗂️ Dataset Organization

The dataset is structured around a central employee-level analytical table:

```text
HR_Analytics
```

Each record represents an employee and contains the attributes required for workforce and employee-experience analysis.

This structure allows the dashboard to analyze employees across multiple dimensions without requiring separate transactional tables.

---

# 📊 Analytical Categories

For dashboard development, the available fields can be conceptually organized into several analytical categories.

## 1. Workforce Demographics

Used to understand the composition of the workforce.

Relevant fields include:

* Age
* AgeGroup
* Gender
* MaritalStatus
* Education
* EducationField

These fields support visuals such as:

* Employee count by age group
* Gender distribution
* Education field distribution
* Marital status distribution
* Average age

---

## 2. Organizational Structure

Used to understand how employees are distributed throughout the organization.

Relevant fields include:

* Department
* JobRole
* JobLevel
* BusinessTravel

These fields support:

* Employee count by department
* Job role distribution
* Job level analysis
* Department comparisons

---

## 3. Compensation

Compensation-related fields support analysis of employee income and salary distribution.

Relevant fields include:

* MonthlyIncome
* MonthlyRate
* DailyRate
* HourlyRate
* SalarySlab
* PercentSalaryHike
* StockOptionLevel

The dashboard uses compensation data to analyze:

* Average monthly income
* Salary slab distribution
* Monthly income by department

---

## 4. Attrition

The `Attrition` field is used to analyze employee turnover.

The dashboard includes:

* Overall attrition rate
* Attrition by department

This allows workforce composition to be viewed alongside employee retention outcomes.

---

## 5. Employee Satisfaction

Employee-experience analysis uses:

* JobSatisfaction
* EnvironmentSatisfaction
* RelationshipSatisfaction
* WorkLifeBalance

These fields are used to compare employee experience across departments.

---

## 6. Performance

The `PerformanceRating` field supports performance analysis.

The dashboard includes:

* Overall average performance rating
* Average performance rating by department

---

## 7. Tenure & Experience

Tenure-related fields include:

* TotalWorkingYears
* YearsAtCompany
* YearsInCurrentRole
* YearsSinceLastPromotion
* YearsWithCurrManager

These fields support employee tenure analysis and contribute to the overall workforce profile.

---

# 📐 Power BI Preparation

The prepared employee dataset was brought into Power BI for analysis and visualization.

The Power BI model centers around:

```text
HR_Analytics
```

The resulting analytical structure provides a single source for the dashboard's workforce, compensation, attrition, satisfaction, and performance analysis.

---

# 🔢 KPI Preparation

The dataset supports several dashboard-level KPIs.

The completed report displays:

| KPI                              | Dashboard Value |
| -------------------------------- | --------------: |
| Total Employees                  |           1.47K |
| Attrition Rate                   |           16.1% |
| Average Monthly Income           |           6.50K |
| Average Tenure                   |            7.01 |
| Average Age                      |              37 |
| Average Job Level                |               2 |
| Average Performance Rating       |            3.15 |
| Average Work-Life Balance        |            2.76 |
| Average Environment Satisfaction |            2.72 |
| Average Job Satisfaction         |            2.68 |

These metrics are calculated and presented through the Power BI analytical layer.

---

# 📊 Preparation for Workforce Analysis

The prepared dataset supports workforce segmentation by:

* Department
* Age group
* Gender
* Education field
* Salary slab
* Job role
* Marital status
* Job level

For example, the dashboard reports:

* Research & Development: 961 employees
* Sales: 446 employees
* Human Resources: 63 employees

This allows workforce concentration to be analyzed at the department level.

---

# 📈 Preparation for Performance Analysis

The dataset provides three major employee-experience dimensions:

```text
Job Satisfaction
Environment Satisfaction
Work-Life Balance
```

These are analyzed alongside:

```text
Performance Rating
```

This allows the Performance section of the dashboard to compare employee experience and performance across departments.

---

# 🔍 Data Quality Considerations

Several fields in the original dataset represent coded or categorical HR attributes.

Examples include:

* Education
* JobLevel
* JobInvolvement
* JobSatisfaction
* EnvironmentSatisfaction
* RelationshipSatisfaction
* PerformanceRating
* WorkLifeBalance
* StockOptionLevel

These fields should be interpreted according to their categorical/rating definitions when analyzing the data.

The dashboard therefore focuses on appropriate aggregations such as:

* Employee counts
* Averages
* Percentages
* Category distributions
* Department comparisons

rather than treating every field as a continuous business metric.

---

# ✅ Outcome

The data preparation stage produced an employee-level analytical dataset suitable for developing the HR Analytics Dashboard.

The prepared data supports analysis across:

**Workforce → Demographics → Compensation → Attrition → Satisfaction → Performance → Tenure**

These analytical dimensions form the foundation for the dashboard presented in the project.
