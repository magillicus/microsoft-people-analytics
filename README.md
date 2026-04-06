# Employee Retention & Engagement Analytics

## Project Overview
Developed an end-to-end people analytics case study translating ambiguous HR business questions into structured analytical solutions, delivering actionable insights on employee attrition and engagement using SQL, Python, and data visualization.

This project simulates the type of workforce analysis an HR Data Analyst and/or People Analytics team might perform to support employee lifecycle decisions. The analysis focuses on identifying patterns in **employee attrition, engagement, promotion history, work arrangement, and survey feedback** to surface actionable insights for HR leadership.

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
- **Python:** Data exploration, validation, and additional analytical support  
- **Excel:** Structured outputs for reporting and visualization prep  
- **Tableau:** Dashboard development and visual storytelling  
- **GitHub:** Project documentation and portfolio presentation  

---

## Dataset
This project uses a **synthetic HR dataset** created specifically for portfolio purposes.

### Tables

**employee_records**
- One row per employee  
- Includes demographic, organizational, engagement, compensation, and attrition fields  

**employee_surveys**
- One to three survey responses per employee  
- Includes satisfaction, work-life balance, and manager effectiveness measures  

### Key Fields
- employee_id  
- department  
- job_role  
- tenure_months  
- salary  
- performance_rating  
- engagement_score  
- promotion_last_2yrs  
- remote_status  
- attrition  
- satisfaction_score  
- work_life_balance_score  
- manager_effectiveness_score  

---

## Analytical Approach

### 1. Data Exploration & Validation
- Validate dataset completeness (row counts, duplicates, nulls)  
- Review value ranges and categorical distributions  
- Confirm join coverage between employee and survey data  

### 2. Metrics Layer Development
Creation of reusable workforce KPIs, including:
- Total employees  
- Attrition count and attrition rate  
- Average engagement score  
- Average tenure  
- Average salary  
- Promotion rate  

### 3. Attrition Analysis
Analysis of attrition trends across:
- Department  
- Job role  
- Tenure band  
- Promotion history  
- Remote status  

### 4. Engagement & Survey Analysis
Evaluation of:
- Engagement by employee segment  
- Relationship between engagement and attrition  
- Latest employee survey sentiment  
- Survey score differences across departments and retention outcomes  

### 5. High-Risk Segment Identification
Identification of employee groups that may warrant targeted HR action based on:
- Higher attrition  
- Lower engagement  
- Lack of recent promotion  
- Weaker employee sentiment  

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
