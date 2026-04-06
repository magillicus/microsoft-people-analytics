-- 1. Average survey scores by department
SELECT
    e.department,
    COUNT(*) AS survey_responses,
    ROUND(AVG(s.satisfaction_score), 2) AS avg_satisfaction_score,
    ROUND(AVG(s.work_life_balance_score), 2) AS avg_work_life_balance_score,
    ROUND(AVG(s.manager_effectiveness_score), 2) AS avg_manager_effectiveness_score
FROM employee_surveys s
JOIN employee_records e
    ON s.employee_id = e.employee_id
GROUP BY e.department
ORDER BY avg_satisfaction_score ASC;


-- 2. Average survey scores by attrition status
SELECT
    e.attrition,
    COUNT(*) AS survey_responses,
    ROUND(AVG(s.satisfaction_score), 2) AS avg_satisfaction_score,
    ROUND(AVG(s.work_life_balance_score), 2) AS avg_work_life_balance_score,
    ROUND(AVG(s.manager_effectiveness_score), 2) AS avg_manager_effectiveness_score
FROM employee_surveys s
JOIN employee_records e
    ON s.employee_id = e.employee_id
GROUP BY e.attrition;


-- 3. Latest survey per employee
WITH latest_survey AS (
    SELECT
        employee_id,
        MAX(survey_date) AS latest_survey_date
    FROM employee_surveys
    GROUP BY employee_id
)
SELECT
    e.employee_id,
    e.department,
    e.job_role,
    e.attrition,
    s.survey_date,
    s.satisfaction_score,
    s.work_life_balance_score,
    s.manager_effectiveness_score
FROM latest_survey ls
JOIN employee_surveys s
    ON ls.employee_id = s.employee_id
   AND ls.latest_survey_date = s.survey_date
JOIN employee_records e
    ON s.employee_id = e.employee_id
LIMIT 50;