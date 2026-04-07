# Employee Retention & Engagement Analytics

## Project Overview
Developed an end-to-end people analytics case study translating ambiguous HR business questions into structured analytical solutions, delivering actionable insights on employee attrition and engagement using SQL, Python, and data visualization.

This project simulates the type of workforce analysis an HR Data Analyst or People Analytics team might perform to support employee lifecycle decisions. The analysis focuses on identifying patterns in **employee attrition, engagement, promotion history, work arrangement, and survey feedback** to surface actionable insights for HR leadership.

---

## Business Problem
A large organization is experiencing inconsistent retention outcomes and varying engagement levels across departments. HR leadership wants to better understand:

- Which employee groups are most at risk of attrition
- How engagement relates to employee retention
- Whether promotion history and work arrangement influence workforce stability
- What survey feedback reveals about employee experience
- Which employee segments should be prioritized for targeted intervention

---

## Project Objectives
This analysis is intended to:

- Measure overall attrition and engagement trends across the workforce
- Identify departments, roles, and tenure groups with elevated attrition risk
- Evaluate how engagement and employee survey feedback relate to retention outcomes
- Highlight high-risk employee segments for HR intervention
- Present findings in a way that supports business decision-making

---

## Tools Used
- **SQL (SQLite):** Data exploration, KPI development, and core analysis
- **Python:** Data validation, exploratory analysis, survey integration, and rule-based risk identification
- **Excel:** Structured outputs for reporting and visualization prep
- **Tableau:** Dashboard development and visual storytelling
- **GitHub:** Project documentation and portfolio presentation

---

## Dataset
This project uses a **synthetic HR dataset** created specifically for portfolio purposes.

### Tables

**employee_records**
- One row per employee
- Includes demographic, organizational, engagement, compensation, promotion, and attrition fields

**employee_surveys**
- One to three survey responses per employee
- Includes satisfaction, work-life balance, and manager effectiveness measures

### Key Fields
- `employee_id`
- `department`
- `job_role`
- `tenure_months`
- `salary`
- `performance_rating`
- `engagement_score`
- `promotion_last_2yrs`
- `remote_status`
- `attrition`
- `satisfaction_score`
- `work_life_balance_score`
- `manager_effectiveness_score`

---

## Analytical Approach

### 1. Data Exploration & Validation
- Validated dataset completeness through row counts, null checks, duplicate checks, and range review
- Confirmed join coverage between employee and survey data

### 2. Metrics Layer Development
Created reusable workforce KPIs including:
- Total employees
- Attrition count and attrition rate
- Average engagement score
- Average tenure
- Average salary
- Promotion rate

### 3. Attrition Analysis
Analyzed attrition trends across:
- Department
- Job role
- Tenure segment
- Promotion history
- Remote status

### 4. Engagement & Survey Analysis
Evaluated:
- Average engagement by attrition status
- Attrition by engagement level
- Latest employee survey sentiment
- Satisfaction, work-life balance, and manager effectiveness by attrition outcome

### 5. High-Risk Employee Identification
Built a simple rule-based risk model using:
- Low engagement
- No recent promotion
- Short tenure
- Lower satisfaction scores

This model identified a small high-risk employee segment with a substantially higher attrition rate than the broader workforce.

---

## Key Insights
- Attrition is highest among employees in their first two years, suggesting onboarding and early employee experience are important retention factors.
- Employees without recent promotions show higher attrition, indicating career progression may be a meaningful driver of retention.
- Lower engagement is strongly associated with higher attrition, making engagement one of the clearest retention signals in the analysis.
- Employees who leave report lower satisfaction, work-life balance, and manager effectiveness scores than those who stay.
- A rule-based high-risk employee segment exhibited more than double the attrition rate of the broader employee population, demonstrating how multiple workforce signals can be combined into a practical retention framework.

---

## Repository Structure

```bash
data/
sql/
python/
excel/
tableau/
presentation/
README.md

```

## Portfolio Purpose

This project is part of a broader portfolio strategy focused on building role-specific analytics case studies. Rather than relying solely on a resume, this repository demonstrates:

- Practical analytical thinking
- Ability to translate workforce data into business insight
