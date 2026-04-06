-- 1. Highest-risk department vs remote status
SELECT
    department,
    remote_status,
    COUNT(*) AS total_employees,
    SUM(CASE WHEN attrition = 'Yes' THEN 1 ELSE 0 END) AS attrition_count,
    ROUND(100.0 * SUM(CASE WHEN attrition = 'Yes' THEN 1 ELSE 0 END) / COUNT(*), 2) AS attrition_rate_pct,
    ROUND(AVG(engagement_score), 2) AS avg_engagement_score
FROM employee_records
GROUP BY department, remote_status
HAVING COUNT(*) >= 75
ORDER BY attrition_rate_pct DESC, avg_engagement_score ASC;

-- 2. Low-engagement employees without recent promotion
SELECT
    department,
    job_role,
    COUNT(*) AS employee_count,
    ROUND(AVG(engagement_score), 2) AS avg_engagement_score,
    ROUND(AVG(tenure_months), 2) AS avg_tenure_months,
    ROUND(100.0 * SUM(CASE WHEN attrition = 'Yes' THEN 1 ELSE 0 END) / COUNT(*), 2) AS attrition_rate_pct
FROM employee_records
WHERE engagement_score < 60
  AND promotion_last_2yrs = 0
GROUP BY department, job_role
HAVING COUNT(*) >= 40
ORDER BY attrition_rate_pct DESC, employee_count DESC;

-- 3. Highest-risk tenure and department segments
SELECT
    department,
    CASE
        WHEN tenure_months < 12 THEN 'Under 1 Year'
        WHEN tenure_months < 24 THEN '1-2 Years'
        WHEN tenure_months < 60 THEN '2-5 Years'
        WHEN tenure_months < 120 THEN '5-10 Years'
        ELSE '10+ Years'
    END AS tenure_bin,
    COUNT(*) AS total_employees,
    ROUND(100.0 * SUM(CASE WHEN attrition = 'Yes' THEN 1 ELSE 0 END) / COUNT(*), 2) AS attrition_rate_pct,
    ROUND(AVG(engagement_score), 2) AS avg_engagement_score
FROM employee_records
GROUP BY department, tenure_bin
HAVING COUNT(*) >= 40
ORDER BY attrition_rate_pct DESC, avg_engagement_score ASC;