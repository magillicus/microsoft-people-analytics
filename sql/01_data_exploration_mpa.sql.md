-- 1. Row counts (both tables)
SELECT COUNT(*) AS employee_row_count
FROM employee_records;

SELECT COUNT(*) AS survey_row_count
FROM employee_surveys;

-- 2. Check for duplicate employee IDs
SELECT employee_id, COUNT(*) AS record_count
FROM employee_records
GROUP BY employee_id
HAVING COUNT(*) > 1;

-- 3. Null checks for key employee fields
SELECT
    SUM(CASE WHEN employee_id IS NULL THEN 1 ELSE 0 END) AS null_employee_id,
    SUM(CASE WHEN department IS NULL THEN 1 ELSE 0 END) AS null_department,
    SUM(CASE WHEN job_role IS NULL THEN 1 ELSE 0 END) AS null_job_role,
    SUM(CASE WHEN tenure_months IS NULL THEN 1 ELSE 0 END) AS null_tenure_months,
    SUM(CASE WHEN salary IS NULL THEN 1 ELSE 0 END) AS null_salary,
    SUM(CASE WHEN engagement_score IS NULL THEN 1 ELSE 0 END) AS null_engagement_score,
    SUM(CASE WHEN attrition IS NULL THEN 1 ELSE 0 END) AS null_attrition
FROM employee_records;

-- 4. Null checks for survey fields
SELECT
    SUM(CASE WHEN survey_id IS NULL THEN 1 ELSE 0 END) AS null_survey_id,
    SUM(CASE WHEN employee_id IS NULL THEN 1 ELSE 0 END) AS null_employee_id,
    SUM(CASE WHEN survey_date IS NULL THEN 1 ELSE 0 END) AS null_survey_date,
    SUM(CASE WHEN satisfaction_score IS NULL THEN 1 ELSE 0 END) AS null_satisfaction_score,
    SUM(CASE WHEN work_life_balance_score IS NULL THEN 1 ELSE 0 END) AS null_work_life_balance_score,
    SUM(CASE WHEN manager_effectiveness_score IS NULL THEN 1 ELSE 0 END) AS null_manager_effectiveness_score
FROM employee_surveys;

-- 5. Value ranges
SELECT
    MIN(age) AS min_age,
    MAX(age) AS max_age,
    MIN(tenure_months) AS min_tenure_months,
    MAX(tenure_months) AS max_tenure_months,
    MIN(salary) AS min_salary,
    MAX(salary) AS max_salary,
    MIN(engagement_score) AS min_engagement_score,
    MAX(engagement_score) AS max_engagement_score
FROM employee_records;

-- 6. Category distributions
SELECT department, COUNT(*) AS employee_count
FROM employee_records
GROUP BY department
ORDER BY employee_count DESC;

SELECT remote_status, COUNT(*) AS employee_count
FROM employee_records
GROUP BY remote_status
ORDER BY employee_count DESC;

SELECT attrition, COUNT(*) AS employee_count
FROM employee_records
GROUP BY attrition;

-- 7. 1:1 Employee to surveys check
SELECT
    COUNT(DISTINCT e.employee_id) AS employees_in_employee_table,
    COUNT(DISTINCT s.employee_id) AS employees_with_surveys
FROM employee_records e
LEFT JOIN employee_surveys s
    ON e.employee_id = s.employee_id;