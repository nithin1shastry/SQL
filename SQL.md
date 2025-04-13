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
