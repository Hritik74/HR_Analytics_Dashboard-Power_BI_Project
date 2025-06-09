# HR Analytics Dashboard – Power BI Project
![Image](https://github.com/user-attachments/assets/a797777f-e334-4a5f-a07c-1edc0b351d15)

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

## 🧮 Measures Created

A wide range of DAX measures were developed to drive the insights in the dashboard. Key measures include:

- **Active Emp** – Calculates the number of currently employed individuals.
- **Attrition Rate** – Dynamic attrition measure using exited vs total employees.
- **Average Salary / Average Bonus amount** – Calculates average compensation metrics.
- **Average Tenure** – Measures how long employees stay on average.
- **Avg Age at Exit** – Analyzes typical age at which employees leave.
- **Avg Salary at Exit** – Helps understand what compensation levels are linked to higher attrition.
- **Gender Ratio** – Measures male vs female proportion within the workforce.
- **Hires per Year / Exits per Year** – Yearly tracking of hiring and attrition events.
- **YoY Change in Headcount, Hiring, Attrition** – Time intelligence metrics comparing current year vs previous year values.
- **Min/Max Active Points** – Captures lowest and peak employee count during a period.
- **BarColor** – A helper measure for conditional formatting of visuals based on performance.

These measures are used across cards, bar charts, KPIs, and trend visuals to enable real-time decision-making.

---

## 📈 Dashboard Features

### 📌 Key Visuals and Charts

- **KPI Cards**: Display key metrics like Active Employees, Attrition Rate, Average Tenure, and Hires/Exits per Year.
- **Line and Area Charts**: 
  - Show attrition and hiring trends year-over-year.
  - Analyze salary and bonus progression over time.
- **Bar & Column Charts**:
  - Distribution of employees across departments, gender, and salary bands.
  - Exits by job title and age buckets.
- **Donut / Pie Charts**: Gender ratio, employment status breakdown.
- **Stacked Column Charts**: Tenure bucket vs attrition or salary level.
- **Matrix Tables**: Show employee counts by department and year with conditional formatting.

### 🎛️ Slicers and Filters

- **Year-Month**, **Gender**, **Department**, **Country**, **Employment Status**, **Salary Band**, and **Tenure Bucket** slicers were added to make the dashboard interactive and customizable for user exploration.

---

### 🔘 Navigation Buttons

- **Navigation buttons** were added to switch between pages:
  - For example, "Next Page", "Previous Page"
- A **bookmark** was used in the dashboard icon to **refresh the page and clear all slicer selections**, allowing users to reset their view.
- These features improve user experience by allowing smooth navigation and easy resetting of filters for a clean exploration experience.

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
### 🔹 **Challenge 2: Multiple Date Columns (Hire & Exit Dates)**  
**Problem**: Both Hire Date and Exit Date needed to be related to the same `DateTable`, but Power BI allows only one active relationship at a time.

**Solution**: Created one active relationship (usually with Hire Date) and used the `USERELATIONSHIP()` function in DAX to calculate metrics like exits over time using Exit Date.

```DAX
Exits per Year = 
CALCULATE(
    COUNTROWS(EmployeesData),
    USERELATIONSHIP(DateTable[Date], EmployeesData[Exit Date])
)
```
### 🔹 **Challenge 3: Sorting Salary Bands and Tenure Buckets**
**Problem**: The visuals displayed the bands and buckets alphabetically instead of in a logical order.

**Solution**: Added a Sort Order column to `SalaryBandTable` and `TenureBucketTable`, then used the "Sort by Column" feature in Power BI to correct the order in charts.

--- 

## 📈 Key Insights Discovered
### The dashboard revealed several important **HR insights**:
- **High Attrition in Specific Years**: A spike in attrition was observed in certain years, helping HR investigate causes like policy changes or organizational shifts.
- **Average Tenure**: The average employee tenure was found to be lower than expected in some departments.
- **Salary vs. Tenure Relationship**: A clear trend showed that employees with longer tenure generally belonged to higher salary bands.
- **Gender Distribution**: Some departments had skewed gender ratios, pointing to potential diversity gaps.
- **Exit Analysis**: The average age and salary at exit indicated that mid-level employees were leaving more frequently than juniors or seniors.
- **Year-over-Year Hiring Trends**: The dashboard exposed fluctuating hiring rates, suggesting seasonal or business-cycle effects.

--- 

🛠 **Tools & Technologies**

- Power BI Desktop  
- Power Query for data transformation  
- DAX for measure creation  
- Relationship modeling & data visualization best practices  

---

📌 **Conclusion**  
This HR Analytics dashboard provides a comprehensive view of workforce dynamics and empowers decision-makers to act on data-backed insights. It is suitable for use by HR professionals, analysts, and leadership to improve retention strategies, monitor hiring practices, and promote workplace diversity.
