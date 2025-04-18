1. https://platform.stratascratch.com/coding/2004-number-of-comments-per-user-in-past-30-days?code_type=3
   
  ```
  SELECT user_id, COUNT(*) AS number_of_comments
  FROM fb_comments_count
  WHERE created_at BETWEEN DATE '2020-01-10' AND DATE '2020-02-10'
  GROUP BY user_id
  HAVING COUNT(*) > 0;
  ```
2. https://platform.stratascratch.com/coding/2006-users-activity-per-month-day?code_type=3
```
SELECT EXTRACT(DAY FROM post_date) AS day_of_month, COUNT(*) AS total_posts
FROM facebook_posts
GROUP BY day_of_month
ORDER BY day_of_month;
```
3. https://platform.stratascratch.com/coding/2009-users-with-two-statuses?code_type=3

```
SELECT user_id
FROM twitch_sessions
WHERE session_type IN ('viewer', 'streamer')
GROUP BY user_id
HAVING COUNT(DISTINCT session_type) = 2;  
```
4. https://platform.stratascratch.com/coding/10308-salaries-differences?code_type=3
```
WITH marketing_salary AS (
   SELECT MAX(emp.salary) AS max_salary
   FROM db_employee emp
   JOIN db_dept dept ON emp.department_id = dept.id
   WHERE dept.department = 'marketing'
),
engineering_salary AS (
   SELECT MAX(emp.salary) AS max_salary
   FROM db_employee emp
   JOIN db_dept dept ON emp.department_id = dept.id
   WHERE dept.department = 'engineering'
 )
SELECT ABS(marketing_salary.max_salary-engineering_salary.max_salary) AS salary_difference
FROM marketing_salary, engineering_salary;
```
5. https://platform.stratascratch.com/coding/10152-workers-with-the-highest-and-lowest-salaries?code_type=1
```
WITH ranked_salaries AS (
   SELECT
      worker_id AS employee_id,
      salary,
      department,
      RANK() OVER (ORDER BY salary DESC) AS rank_desc,
      RANK() OVER (ORDER BY salary ASC) AS rand_asc
   FROM worker
)
SELECT employee_id, salary, department,
       CASE
         WHEN rank_desc = 1 THEN 'Highest Salary'
         WHEN rank_asc = 1 THEN 'Lowest Salary'
      END AS salary_type
FROM ranked_salaries
WHERE rank_desc=1 OR rank_asc=1;

ANOTHER SOLUTION

SELECT 
    worker_id AS employee_id,
    salary,
    department,
    'Highest Salary' AS salary_type
FROM worker
WHERE salary = (SELECT MAX(salary) FROM worker)

UNION ALL

SELECT 
    worker_id AS employee_id,
    salary,
    department,
    'Lowest Salary' AS salary_type
FROM worker
WHERE salary = (SELECT MIN(salary) FROM worker);



```

