-- 1. Average engagement by department
SELECT
    department,
    COUNT(*) AS total_employees,
    ROUND(AVG(engagement_score), 2) AS avg_engagement_score
FROM employee_records
GROUP BY department
ORDER BY avg_engagement_score ASC;


-- 2. Average engagement by attrition status
SELECT
    attrition,
    COUNT(*) AS total_employees,
    ROUND(AVG(engagement_score), 2) AS avg_engagement_score
FROM employee_records
GROUP BY attrition;


-- 3. Engagement (bins) vs attrition
SELECT
    CASE
        WHEN engagement_score < 50 THEN 'Low (<50)'
        WHEN engagement_score < 65 THEN 'Moderate (50-64)'
        WHEN engagement_score < 80 THEN 'High (65-79)'
        ELSE 'Very High (80+)'
    END AS engagement_bin,
    COUNT(*) AS total_employees,
    SUM(CASE WHEN attrition = 'Yes' THEN 1 ELSE 0 END) AS attrition_count,
    ROUND(100.0 * SUM(CASE WHEN attrition = 'Yes' THEN 1 ELSE 0 END) / COUNT(*), 2) AS attrition_rate_pct
FROM employee_records
GROUP BY engagement_bin
ORDER BY
    CASE engagement_bin
        WHEN 'Low (<50)' THEN 1
        WHEN 'Moderate (50-64)' THEN 2
        WHEN 'High (65-79)' THEN 3
        ELSE 4
    END;


-- 4. Engagement by remote status
SELECT
    remote_status,
    COUNT(*) AS total_employees,
    ROUND(AVG(engagement_score), 2) AS avg_engagement_score
FROM employee_records
GROUP BY remote_status
ORDER BY avg_engagement_score ASC;


-- 5. Engagement by tenure bin
SELECT
    CASE
        WHEN tenure_months < 12 THEN 'Under 1 Year'
        WHEN tenure_months < 24 THEN '1-2 Years'
        WHEN tenure_months < 60 THEN '2-5 Years'
        WHEN tenure_months < 120 THEN '5-10 Years'
        ELSE '10+ Years'
    END AS tenure_bin,
    COUNT(*) AS total_employees,
    ROUND(AVG(engagement_score), 2) AS avg_engagement_score
FROM employee_records
GROUP BY tenure_bin
ORDER BY
    CASE tenure_bin
        WHEN 'Under 1 Year' THEN 1
        WHEN '1-2 Years' THEN 2
        WHEN '2-5 Years' THEN 3
        WHEN '5-10 Years' THEN 4
        ELSE 5
    END;