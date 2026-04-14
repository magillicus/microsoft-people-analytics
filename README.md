# Employee Retention & Engagement Analytics

## Overview
End-to-end people analytics case study analyzing employee attrition and engagement to identify workforce risk drivers and deliver actionable HR insights using SQL, Python, and Tableau.

This project simulates a real-world HR analytics scenario, translating workforce data into business recommendations focused on improving employee retention.

## Dashboard Preview
<img width="949" height="524" alt="People Analytics Dashboard Screenshot" src="https://github.com/user-attachments/assets/297e24e4-d67e-46de-a7c6-3ab37f1a023b" />

## Executive Summary Presentation
[AIrsoft Employee Attrition and Engagement Analysis Deck.pdf](https://github.com/user-attachments/files/26666798/AIrsoft.Employee.Attrition.and.Engagement.Analysis.Deck.pdf)

---

## Key Insights
- Employees in their first two years exhibit the highest attrition rates, indicating onboarding and early experience as critical retention factors.
- Employees without recent promotions are more likely to leave, suggesting gaps in career progression.
- Lower engagement scores are strongly associated with higher attrition, making engagement a key retention lever.
- Employees who leave report consistently lower satisfaction, work-life balance, and manager effectiveness scores.
- A rule-based high-risk employee segment shows more than **2x higher attrition** than the overall workforce.

---

## Business Impact
This analysis demonstrates how HR teams can:
- Identify high-risk employees before they leave
- Prioritize retention efforts by department and employee segment
- Improve engagement and employee experience to reduce turnover
- Apply data-driven decision-making to workforce strategy

---

## Tools & Skills Demonstrated
- **SQL (SQLite):** Data exploration, KPI development, segmentation analysis  
- **Python:** Data validation, feature engineering, segmentation, and risk modeling  
- **Tableau:** Dashboard design and visual storytelling *(in progress)*  
- **Excel:** Data structuring and reporting outputs  
- **Analytics Skills:** Cohort analysis, segmentation, metric development, business insight generation  

---

## Dataset
Synthetic HR dataset designed to replicate real-world workforce analytics scenarios.

**Tables:**
- `employee_records` – employee demographics, compensation, engagement, and attrition
- `employee_surveys` – satisfaction, work-life balance, and manager effectiveness scores

---

## Analytical Approach
1. Data validation and exploration  
2. KPI and metrics layer development  
3. Attrition analysis by department, tenure, and promotion history  
4. Engagement and survey sentiment analysis  
5. Rule-based high-risk employee identification  

---

## Repository Structure
```bash
data/
    data_dictionary.txt
    employee_records.csv
    employee_surveys.csv
    microsoft_people_analytics.sqlite
sql/
    01_data_exploration_mpa.sql.md
    02_metrics_layer_mpa.sql.md
    03_attrition_analysis.sql.md
    04_engagement_and_survey_analysis.sql.md
    05_high_risk_segment_analysis.sql.md
python/
    01_people_analytics_exploration.ipynb
excel/
    people_analytics_outputs.xlsx
tableau/
    HR People Analytics Dashboard.twb
presentation/
    AIrsoft Employee Attrition and Engagement Deck.pdf
README.md
```

## Portfolio Purpose

This project is part of a broader portfolio strategy focused on building role-specific analytics case studies. Rather than relying solely on a resume, this repository demonstrates:

- Practical analytical thinking
- Ability to translate workforce data into business insight
