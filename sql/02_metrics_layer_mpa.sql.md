/*
File: 02_metrics_layer.sql
Purpose: Define core people analytics KPIs and reusable summary views
Project: Microsoft HR Data Analyst, People Analytics Portfolio Project
Author: Marcus Gillis
*/

-- 1. Core KPIs
SELECT
    COUNT(*) AS total_employees,
    SUM(CASE WHEN attrition = 'Yes' THEN 1 ELSE 0 END) AS attrition_count,
    ROUND(
        100.0 * SUM(CASE WHEN attrition = 'Yes' THEN 1 ELSE 0 END) / COUNT(*),
        2
    ) AS attrition_rate_pct,
    ROUND(AVG(engagement_score), 2) AS avg_engagement_score,
    ROUND(AVG(tenure_months), 2) AS avg_tenure_months,
    ROUND(AVG(salary), 2) AS avg_salary,
    ROUND(100.0 * AVG(promotion_last_2yrs), 2) AS promotion_rate_pct
FROM employee_records;


-- 2. KPI summary by department
SELECT
    department,
    COUNT(*) AS total_employees,
    SUM(CASE WHEN attrition = 'Yes' THEN 1 ELSE 0 END) AS attrition_count,
    ROUND(
        100.0 * SUM(CASE WHEN attrition = 'Yes' THEN 1 ELSE 0 END) / COUNT(*),
        2
    ) AS attrition_rate_pct,
    ROUND(AVG(engagement_score), 2) AS avg_engagement_score,
    ROUND(AVG(tenure_months), 2) AS avg_tenure_months,
    ROUND(AVG(salary), 2) AS avg_salary,
    ROUND(100.0 * AVG(promotion_last_2yrs), 2) AS promotion_rate_pct
FROM employee_records
GROUP BY department
ORDER BY attrition_rate_pct DESC;


-- 3. KPI summary by remote status
SELECT
    remote_status,
    COUNT(*) AS total_employees,
    SUM(CASE WHEN attrition = 'Yes' THEN 1 ELSE 0 END) AS attrition_count,
    ROUND(
        100.0 * SUM(CASE WHEN attrition = 'Yes' THEN 1 ELSE 0 END) / COUNT(*),
        2
    ) AS attrition_rate_pct,
    ROUND(AVG(engagement_score), 2) AS avg_engagement_score,
    ROUND(AVG(tenure_months), 2) AS avg_tenure_months,
    ROUND(AVG(salary), 2) AS avg_salary
FROM employee_records
GROUP BY remote_status
ORDER BY attrition_rate_pct DESC;


-- 4. KPI summary by performance rating
SELECT
    performance_rating,
    COUNT(*) AS total_employees,
    ROUND(100.0 * SUM(CASE WHEN attrition = 'Yes' THEN 1 ELSE 0 END) / COUNT(*), 2) AS attrition_rate_pct,
    ROUND(AVG(engagement_score), 2) AS avg_engagement_score,
    ROUND(AVG(salary), 2) AS avg_salary
FROM employee_records
GROUP BY performance_rating
ORDER BY performance_rating;