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
SELECT 
    d.account_id,
    (COUNT(DISTINCT CASE WHEN record_date BETWEEN '2021-01-01' AND '2021-01-31' THEN user_id END) * 1.0 / 
     COUNT(DISTINCT CASE WHEN record_date BETWEEN '2020-12-01' AND '2020-12-31' THEN user_id END)) AS growth_rate
FROM sf_events d
GROUP BY d.account_id;

```
15. https://platform.stratascratch.com/coding/2056-number-of-shipments-per-month?code_type=3
```
select count(shipment_id), DATE_FORMAT(shipment_date, '%Y-%m')  date_ym
from amazon_shipment
group by date_ym;
```
16. https://platform.stratascratch.com/coding/2057-weight-for-first-shipment?code_type=3
```
SELECT shipment_id, weight
FROM amazon_shipment
GROUP BY shipment_id
HAVING MIN(shipment_date);
```
17. https://platform.stratascratch.com/coding/2058-total-shipment-weight?code_type=3
```
SELECT 
    shipment_id, 
    sub_id, 
    weight, 
    shipment_date, 
    SUM(weight) OVER (PARTITION BY shipment_id) AS total_weight
FROM amazon_shipment;
```
18. https://platform.stratascratch.com/coding/2061-users-with-many-searches?code_type=3
```
SELECT COUNT(DISTINCT user_id) AS num_users
FROM fb_searches
WHERE YEAR(date) = 2021 AND MONTH(date) = 8
GROUP BY user_id
HAVING COUNT(search_id) > 5;
```
19. https://platform.stratascratch.com/coding/2062-questions-in-second-quarter?code_type=3
```
SELECT COUNT(search_id)
FROM fb_searches
WHERE date BETWEEN '2021-04-01' AND '2021-08-30';
```
20. https://platform.stratascratch.com/coding/2063-change-of-currency-exchange-rates?code_type=3
```
WITH jan_exchange_rate AS (
    SELECT source_currency, exchange_rate AS jan_rate
    FROM sf_exchange_rate
    WHERE date = '2020-01-01'
),
july_exchange_rate AS (
    SELECT source_currency, exchange_rate AS july_rate
    FROM sf_exchange_rate
    WHERE date = '2020-07-01'
)

SELECT 
    e1.source_currency, 
    (e2.july_rate - e1.jan_rate) AS diff_currency
FROM jan_exchange_rate e1
JOIN july_exchange_rate e2
    ON e1.source_currency = e2.source_currency;

```
21. https://platform.stratascratch.com/coding/2067-low-fat-and-recyclable?code_type=3
```
SELECT 
    (COUNT(CASE 
            WHEN is_low_fat = 'Y' AND is_recyclable = 'Y' 
            THEN 1 END) * 100.0) / COUNT(*) AS percentage_low_fat_and_recyclable
FROM facebook_products;

```
22. https://platform.stratascratch.com/coding/2069-sales-with-valid-promotion?code_type=3
```
SELECT 
    (COUNT(DISTINCT o.product_id) * 100.0) / (SELECT COUNT(*) FROM online_orders) AS promotion_percentage
FROM 
    online_orders o
JOIN 
    online_promotions p
ON 
    o.promotion_id = p.promotion_id;

```





