## Difference between WHERE and Having - interview point of view notes

==> WHERE clause cannot be used with aggregates where as HAVING can. This means WHERE clause is used for filtering individual rows where as HAVING clause is used to filter groups.

==> WHERE comes before GROUP BY. This means WHERE clause filters rows before aggregate calculations are performed. HAVING comes after GROUP BY. This means HAVING clause filters rows after aggregate calculations are performed. So from a performance standpoint, HAVING is slower than WHERE and should be avoided when possible.

==> WHERE and HAVING can be used together in a SELECT query. In this case WHERE clause is applied first to filter individual rows. The rows are then grouped and aggregate calculations are performed, and then the HAVING clause filters the groups.

==> So from a performance standpoint, HAVING is slower than WHERE and should be avoided when possible.

==> Another difference is WHERE comes before GROUP BY and HAVING comes after GROUP BY.

## SQL Convert Rows to Columns and Columns to Rows without using Pivot Functions

| emp_id | salary_component_type | val   |
| ------ | --------------------- | ----- |
| 1      | salary                | 10000 |
| 1      | bonus                 | 5000  |
| 1      | hike_percent          | 10    |
| 2      | salary                | 20000 |
| 2      | bonus                 | 1000  |
| 2      | hike_percent          | 20    |

![Screenshot 2025-04-13 at 3 21 19 PM](https://github.com/user-attachments/assets/914296b7-1a6b-437b-a8fc-446e42269924)


![Screenshot 2025-04-13 at 3 21 52 PM](https://github.com/user-attachments/assets/74dabb7c-c1ed-4b00-9a94-89395df2996b)


![Screenshot 2025-04-13 at 3 23 16 PM](https://github.com/user-attachments/assets/8493b13c-9094-4663-8c3a-2d07ea131fdd)

## Top 10 SQL interview Q's and Answers
1. How to find duplicates in a given table
   ```
   SELECT emp_id, COUNT(1) from emp group by emp_id having COUNT(1)>1;
   ```
2. How to delete duplicates
  ```
  with CTE AS (SELECT *, row_number() OVER (PARTITION BY emp_id order by emp_id) AS rn from emp1)
  DELETE FROM cte WHERE rn > 1;

  ```
3. Difference between Union and union all
   - Suppose if I have 8 records in table 1 and 9 records in table 2 where table 2 has one duplicate record, union all will get 17 records (all from first + all from second)
   - union will give unique values, remove duplicate
   ![Screenshot 2025-04-14 at 4 58 53 PM](https://github.com/user-attachments/assets/f874b91e-f3ad-4f75-ac85-dccda3ad7216)

   ![Screenshot 2025-04-14 at 4 59 03 PM](https://github.com/user-attachments/assets/b012cbe9-472c-4a84-900c-23265a0f3cbf)

   ![Screenshot 2025-04-14 at 4 59 33 PM](https://github.com/user-attachments/assets/f29a63bc-d15f-4b01-a3ed-d2646287a7b4)

4. Difference between rank, row_number and dense_rank
5. Employees who are not present in department table
   ![Screenshot 2025-04-14 at 5 01 05 PM](https://github.com/user-attachments/assets/a43f6810-6c14-4e11-9d82-227ea730e014)

   In the above screenshot, emp from dept 100, 300 are there in dept table but not 200 and 900

   ```
   SELECT * FROM emp WHERE department_id NOT IN (SELECT dept_id FROM dept);
   ```
   Sub queries are not efficient

   ```
   SELECT emp.*, dept.dep_id, dept.dep_name FROM emp
   LEFT JOIN dept
   ON emp.department_id = dept.dep_id
   WHERE dept.dep_name IS NULL
   ```
   ![Screenshot 2025-04-14 at 5 07 15 PM](https://github.com/user-attachments/assets/14e3cd93-293e-493f-89b3-13612379dda3)

  ![Screenshot 2025-04-14 at 5 07 41 PM](https://github.com/user-attachments/assets/87f010d9-3ae5-4b7e-8b62-6b5aa7c02298)

  
6. Second highest Salary in each department.
   **RANK() will skip the next rank if there is a tie in data, so if you have two rank 1's, the next rank will be rank 3. DENSE_RANK() will not permit gaps in ranks and will always increment even if there is a tie. So if you have two rank 1's, the next rank will always be rank 2**

   ![Screenshot 2025-04-14 at 5 14 26 PM](https://github.com/user-attachments/assets/29e9c720-a8af-4c8f-9da2-ab506dab04be)

   ![Screenshot 2025-04-14 at 5 14 36 PM](https://github.com/user-attachments/assets/79f5d7fe-c71e-4ec0-ad39-e253436f0065)

   ![Screenshot 2025-04-14 at 5 14 54 PM](https://github.com/user-attachments/assets/a69e0d22-c115-479a-be30-21a71e0cf3df)

   ![Screenshot 2025-04-14 at 5 17 14 PM](https://github.com/user-attachments/assets/9b82fe20-2712-4980-9606-f6e75d6738c7)

   





  



