/*
File: 01_data_exploration.sql
Purpose: Perform initial data validation, structure review, and exploratory checks
Project: Microsoft HR Data Analyst, People Analytics Portfolio Project
Author: Marcus Gillis
*/

-- 1. Row count confirmation (both tables)
SELECT COUNT(*) AS employee_row_count
FROM employee_records;

SELECT COUNT(*) AS survey_row_count
FROM employee_surveys;

-- 2. Preview employee_records
SELECT *
FROM employee_records
LIMIT 10;

-- 3. Preview employee_surveys
SELECT *
FROM employee_surveys
LIMIT 10;

-- 4. Check for duplicate employee IDs in employee_records
SELECT employee_id, COUNT(*) AS record_count
FROM employee_records
GROUP BY employee_id
HAVING COUNT(*) > 1;

-- 5. Null checks for key employee fields
SELECT
    SUM(CASE WHEN employee_id IS NULL THEN 1 ELSE 0 END) AS null_employee_id,
    SUM(CASE WHEN department IS NULL THEN 1 ELSE 0 END) AS null_department,
    SUM(CASE WHEN job_role IS NULL THEN 1 ELSE 0 END) AS null_job_role,
    SUM(CASE WHEN tenure_months IS NULL THEN 1 ELSE 0 END) AS null_tenure_months,
    SUM(CASE WHEN salary IS NULL THEN 1 ELSE 0 END) AS null_salary,
    SUM(CASE WHEN engagement_score IS NULL THEN 1 ELSE 0 END) AS null_engagement_score,
    SUM(CASE WHEN attrition IS NULL THEN 1 ELSE 0 END) AS null_attrition
FROM employee_records;

-- 6. Null checks for survey fields
SELECT
    SUM(CASE WHEN survey_id IS NULL THEN 1 ELSE 0 END) AS null_survey_id,
    SUM(CASE WHEN employee_id IS NULL THEN 1 ELSE 0 END) AS null_employee_id,
    SUM(CASE WHEN survey_date IS NULL THEN 1 ELSE 0 END) AS null_survey_date,
    SUM(CASE WHEN satisfaction_score IS NULL THEN 1 ELSE 0 END) AS null_satisfaction_score,
    SUM(CASE WHEN work_life_balance_score IS NULL THEN 1 ELSE 0 END) AS null_work_life_balance_score,
    SUM(CASE WHEN manager_effectiveness_score IS NULL THEN 1 ELSE 0 END) AS null_manager_effectiveness_score
FROM employee_surveys;


-- 7. Distinct dimensions
SELECT DISTINCT department
FROM employee_records
ORDER BY department;

SELECT DISTINCT remote_status
FROM employee_records
ORDER BY remote_status;

SELECT DISTINCT attrition
FROM employee_records
ORDER BY attrition;

SELECT DISTINCT performance_rating
FROM employee_records
ORDER BY performance_rating;


-- 8. Value ranges
SELECT
    MIN(age) AS min_age,
    MAX(age) AS max_age,
    MIN(tenure_months) AS min_tenure,
    MAX(tenure_months) AS max_tenure,
    MIN(salary) AS min_salary,
    MAX(salary) AS max_salary,
    MIN(engagement_score) AS min_engagement,
    MAX(engagement_score) AS max_engagement
FROM employee_records;


-- 9. Employee count by department
SELECT
    department,
    COUNT(*) AS employee_count
FROM employee_records
GROUP BY department
ORDER BY employee_count DESC;


-- 10. Employee distribution by remote status
SELECT
    remote_status,
    COUNT(*) AS employee_count
FROM employee_records
GROUP BY remote_status
ORDER BY employee_count DESC;


-- 11. Attrition distribution
SELECT
    attrition,
    COUNT(*) AS employee_count
FROM employee_records
GROUP BY attrition;


-- 12. Validate table join coverage
SELECT
    COUNT(DISTINCT e.employee_id) AS employees_in_employee_table,
    COUNT(DISTINCT s.employee_id) AS employees_in_survey_table
FROM employee_records e
LEFT JOIN employee_surveys s
    ON e.employee_id = s.employee_id;


-- 13. Survey response count per employee
SELECT
    employee_id,
    COUNT(*) AS survey_count
FROM employee_surveys
GROUP BY employee_id
ORDER BY survey_count DESC, employee_id
LIMIT 20;