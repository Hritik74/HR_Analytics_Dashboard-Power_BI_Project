# HR Analytics Dashboard – Power BI Project

## 📌 Problem Statement

In many organizations, HR teams struggle to get timely, data-driven insights into employee behavior, attrition trends, tenure distribution, and salary analysis. The lack of a centralized system to visualize key HR metrics limits their ability to take proactive decisions.

This project addresses that challenge by creating an interactive Power BI dashboard to monitor and analyze workforce data. It helps identify critical trends in attrition, hiring, tenure, salary distribution, and diversity—enabling better workforce planning and decision-making.

---

## 📊 Dataset & Data Model

### 📂 Dataset Overview

The primary dataset used is an anonymized employee-level dataset containing information such as:
- Employee Age, Gender, Job Title, Department
- Hire Date and Exit Date
- Employment Status (Active/Exited)
- Annual Salary, Bonus Percentage
- Country, Business Unit, and City
- Tenure in years and categorized buckets
- Salary Band classification

### 🧱 Data Model Design

The data model consists of the following tables:

1. **EmployeesData** – Main fact table containing employee-level details.
2. **DateTable** – Custom date table to enable robust time intelligence.
3. **SalaryBandTable** – Lookup table to group employees by salary bands.
4. **TenureBucketTable** – Lookup table to classify tenure ranges.
5. **_Measures** – DAX measures used for KPIs and calculations.

#### 🔗 Relationships:
- `DateTable[Date]` → `EmployeesData[Hire Date]` and `Exit Date`
- `SalaryBandTable[Salary Band]` → `EmployeesData[Salary Band]`
- `TenureBucketTable[Tenure Bucket]` → `EmployeesData[Tenure Bucket]`

The relationships are set up as one-to-many, with lookup tables on the one-side and EmployeesData on the many-side.

---

## ✅ Challenges & Resolutions

### 🔹 Challenge 1: Attrition Rate Calculation
**Problem:** Employees without exit dates are still active, and calculating attrition by year required filtering only exited employees.

**Solution:** A measure was created using DAX to calculate attrition only for employees with exit dates in the selected period.

```DAX
Attrition Rate = 
DIVIDE(
    [Exited Emp],
    [Total Employees],
    0
)
```
