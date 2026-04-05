-- 1. Attrition by department
SELECT
    department,
    COUNT(*) AS total_employees,
    SUM(CASE WHEN attrition = 'Yes' THEN 1 ELSE 0 END) AS attrition_count,
    ROUND(100.0 * SUM(CASE WHEN attrition = 'Yes' THEN 1 ELSE 0 END) / COUNT(*), 2) AS attrition_rate_pct
FROM employee_records
GROUP BY department
ORDER BY attrition_rate_pct DESC;


-- 2. Attrition by job role
SELECT
    job_role,
    COUNT(*) AS total_employees,
    SUM(CASE WHEN attrition = 'Yes' THEN 1 ELSE 0 END) AS attrition_count,
    ROUND(100.0 * SUM(CASE WHEN attrition = 'Yes' THEN 1 ELSE 0 END) / COUNT(*), 2) AS attrition_rate_pct
FROM employee_records
GROUP BY job_role
HAVING COUNT(*) >= 100
ORDER BY attrition_rate_pct DESC, total_employees DESC;


-- 3. Attrition by tenure (bins)
SELECT
    CASE
        WHEN tenure_months < 12 THEN 'Under 1 Year'
        WHEN tenure_months < 24 THEN '1-2 Years'
        WHEN tenure_months < 60 THEN '2-5 Years'
        WHEN tenure_months < 120 THEN '5-10 Years'
        ELSE '10+ Years'
    END AS tenure_bin,
    COUNT(*) AS total_employees,
    SUM(CASE WHEN attrition = 'Yes' THEN 1 ELSE 0 END) AS attrition_count,
    ROUND(100.0 * SUM(CASE WHEN attrition = 'Yes' THEN 1 ELSE 0 END) / COUNT(*), 2) AS attrition_rate_pct
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


-- 4. Attrition by promotion history
SELECT
    promotion_last_2yrs,
    COUNT(*) AS total_employees,
    SUM(CASE WHEN attrition = 'Yes' THEN 1 ELSE 0 END) AS attrition_count,
    ROUND(100.0 * SUM(CASE WHEN attrition = 'Yes' THEN 1 ELSE 0 END) / COUNT(*), 2) AS attrition_rate_pct
FROM employee_records
GROUP BY promotion_last_2yrs;


-- 5. Attrition by remote status
SELECT
    remote_status,
    COUNT(*) AS total_employees,
    SUM(CASE WHEN attrition = 'Yes' THEN 1 ELSE 0 END) AS attrition_count,
    ROUND(100.0 * SUM(CASE WHEN attrition = 'Yes' THEN 1 ELSE 0 END) / COUNT(*), 2) AS attrition_rate_pct
FROM employee_records
GROUP BY remote_status
ORDER BY attrition_rate_pct DESC;