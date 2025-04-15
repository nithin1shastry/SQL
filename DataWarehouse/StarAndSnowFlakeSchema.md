![Screenshot 2025-04-14 at 7 52 21 PM](https://github.com/user-attachments/assets/0c368dfb-7ad7-4a9a-88a7-255bbe92c534)

- Star schema - Dimensions table is denormalized and contain redundant data
- Snowflake schema - Dim table is normalized and no redundant data is present
- If facts constitute majority of data -> STAR
- If Dim is huge -> Snowflake


  ![Screenshot 2025-04-14 at 7 54 10 PM](https://github.com/user-attachments/assets/a8dc04aa-193d-41a4-a5fe-c84b030e1927)

  ![Screenshot 2025-04-14 at 7 54 52 PM](https://github.com/user-attachments/assets/f1c26f93-dc0c-4501-b910-1bb9b9357c1a)

  ![Screenshot 2025-04-14 at 7 57 56 PM](https://github.com/user-attachments/assets/57186101-8503-430e-9d7d-c766243f2161)

  ![Screenshot 2025-04-14 at 7 59 14 PM](https://github.com/user-attachments/assets/c6005618-e8e3-4c41-9c52-c12fd2958807)


Great question — this is often asked in interviews, especially when discussing **data warehousing** or **reporting systems**.

---

### 🔹 Why does a **denormalized table** contain redundant values?

> A **denormalized table** contains **redundant (repeated) values** because it combines data from multiple related tables — often by **joining dimension tables into the fact table** — to improve **read performance and simplify querying**.

---

### ✅ Example:

Imagine you have normalized tables like this:

#### Customer Table (Dimension):
| Customer_ID | Name   | City     |
|-------------|--------|----------|
| 1           | Alice  | New York |
| 2           | Bob    | Chicago  |

#### Sales Table (Fact):
| Sale_ID | Customer_ID | Amount |
|---------|-------------|--------|
| 101     | 1           | 200    |
| 102     | 2           | 150    |
| 103     | 1           | 300    |

Now if we **denormalize**, we join customer info into the sales table:

#### Denormalized Sales Table:
| Sale_ID | Customer_ID | Name   | City     | Amount |
|---------|-------------|--------|----------|--------|
| 101     | 1           | Alice  | New York | 200    |
| 102     | 2           | Bob    | Chicago  | 150    |
| 103     | 1           | Alice  | New York | 300    |

Notice how **“Alice” and “New York” are repeated** — that’s **redundant**, but it allows you to query everything in one place without joins.

---

### 🎯 Interview-friendly explanation:

> "Denormalized tables contain redundant values because they combine data from multiple normalized tables into one. This avoids complex joins and improves query performance, especially for reporting and analytics. While it increases storage and can lead to data duplication, it speeds up read-heavy operations, which is often the goal in data warehousing."

---

"In ETL, we load dimension tables first because fact tables rely on them. Fact tables store foreign keys that reference dimensions, so if the dimensions aren't loaded first, the fact data can’t properly connect. Loading dimensions first ensures referential integrity and allows us to accurately map relationships."





