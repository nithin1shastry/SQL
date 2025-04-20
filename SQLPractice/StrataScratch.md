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
6. https://platform.stratascratch.com/coding/2013-customer-average-orders?code_type=3
```
SELECT COUNT(DISTINCT customer_id), AVG(amount) FROM postmates_orders;
```

7. https://platform.stratascratch.com/coding/2017-paid-users-in-april-2020?code_type=3

```
   SELECT COUNT(DISTINCT c.user_id)
   FROM rc_calls c
   JOIN rc_users u ON c.user_id = u.user_id
   WHERE u.status = 'paid'
      AND c.call_date >= '2020-04-01'
      AND c.call_date < '2020-05-01';
```
8. https://platform.stratascratch.com/coding/2018-inactive-free-users?code_type=3

```
   SELECT c.user_id
   FROM rc_calls c
   JOIN rc_users u ON c.user_id = u.user_id
   WHERE u.status = 'free'
   AND c.call_date < '2020-04-01' OR c.call_date >= '2020-05-01';
```
9. https://platform.stratascratch.com/coding/2024-unique-users-per-client-per-month?code_type=3
```
SELECT client_id,
       MONTH(time_id) as month,
       COUNT(DISTINCT user_id) as users_num
FROM fact_events
GROUP BY client_id,
          MONTH(time_id)
```
10. https://platform.stratascratch.com/coding/2039-products-report-summary?code_type=3
```
SELECT 
    p.product_category,
    COUNT(DISTINCT t.transaction_id) AS number_of_transactions,
    SUM(t.sales) AS total_sales
FROM wfm_transactions t
JOIN wfm_products p ON t.product_id = p.product_id
WHERE YEAR(t.transaction_date) = 2017
GROUP BY p.product_category
HAVING SUM(t.sales) > 0
ORDER BY total_sales DESC;
```

11. https://platform.stratascratch.com/coding/2043-employees-without-annual-review?code_type=3

```
SELECT ue.first_name, ue.last_name, ue.hire_date, ue.termination_date
FROM uber_employees ue
LEFT JOIN uber_annual_review r ON ue.id = r.emp_id
WHERE r.emp_id IS NULL
ORDER BY ue.hire_date DESC;

```
12. https://platform.stratascratch.com/coding/2049-total-order-per-status-per-service?code_type=3
```
SELECT
    service_name,
    order_status,
    COUNT(*) AS total_orders
FROM
    orders
GROUP BY
    service_name,
    order_status;

```
13. https://platform.stratascratch.com/coding/2051-monthly-active-users?code_type=3
```
SELECT account_id, COUNT(DISTINCT user_id) AS distinct_user_count
FROM sf_events
WHERE YEAR(record_date) = 2021 AND MONTH(record_date) = 1
GROUP BY account_id;
```
14. https://platform.stratascratch.com/coding/2052-user-growth-rate?code_type=3
```
WITH 
```



