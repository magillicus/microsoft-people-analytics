-- 1. Average engagement by attrition status
SELECT
    attrition,
    COUNT(*) AS total_employees,
    ROUND(AVG(engagement_score), 2) AS avg_engagement_score
FROM employee_records
GROUP BY attrition;

-- 2. Engagement (bins) vs attrition
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

-- 3. Average engagement by department
SELECT
    department,
    COUNT(*) AS total_employees,
    ROUND(AVG(engagement_score), 2) AS avg_engagement_score
FROM employee_records
GROUP BY department
ORDER BY avg_engagement_score ASC;

-- 4. Most recent survey vs attrition status (w/ employee context)
WITH latest_survey AS (
    SELECT
        employee_id,
        MAX(survey_date) AS latest_survey_date
    FROM employee_surveys
    GROUP BY employee_id
),
latest_employee_survey AS (
    SELECT
        e.employee_id,
        e.department,
        e.remote_status,
        e.attrition,
        s.satisfaction_score,
        s.work_life_balance_score,
        s.manager_effectiveness_score
    FROM latest_survey ls
    JOIN employee_surveys s
        ON ls.employee_id = s.employee_id
       AND ls.latest_survey_date = s.survey_date
    JOIN employee_records e
        ON e.employee_id = s.employee_id
)
SELECT
    attrition,
    COUNT(*) AS employee_count,
    ROUND(AVG(satisfaction_score), 2) AS avg_satisfaction_score,
    ROUND(AVG(work_life_balance_score), 2) AS avg_work_life_balance_score,
    ROUND(AVG(manager_effectiveness_score), 2) AS avg_manager_effectiveness_score
FROM latest_employee_survey
GROUP BY attrition
ORDER BY attrition;

-- 5. Most recent survey scores by department
WITH latest_survey AS (
    SELECT
        employee_id,
        MAX(survey_date) AS latest_survey_date
    FROM employee_surveys
    GROUP BY employee_id
),
latest_employee_survey AS (
    SELECT
        e.department,
        e.attrition,
        s.satisfaction_score,
        s.work_life_balance_score,
        s.manager_effectiveness_score
    FROM latest_survey ls
    JOIN employee_surveys s
        ON ls.employee_id = s.employee_id
       AND ls.latest_survey_date = s.survey_date
    JOIN employee_records e
        ON e.employee_id = s.employee_id
)
SELECT
    department,
    COUNT(*) AS employee_count,
    ROUND(AVG(satisfaction_score), 2) AS avg_satisfaction_score,
    ROUND(AVG(work_life_balance_score), 2) AS avg_work_life_balance_score,
    ROUND(AVG(manager_effectiveness_score), 2) AS avg_manager_effectiveness_score
FROM latest_employee_survey
GROUP BY department
ORDER BY avg_satisfaction_score ASC;