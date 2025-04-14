Resource - https://www.youtube.com/playlist?list=PLUWdEQb_2yqX21c8Wv6ai0yZ93cQSnDJg

## Fact tables and types of fact tables
- Not every fact table will have surrogate key
  
- Surrogate key - A surrogate key is a unique identifier for a record in a table that has no business meaning — it's purely used for uniquely identifying each row.
In Simple Terms:
It’s like a system-generated ID (like an auto-increment number) that the database assigns to each row, instead of using a natural or real-world value.

- Degenerate dimension - A Degenerate Dimension is a dimension-like piece of data stored in a fact table, but it doesn’t have its own dimension table.

It’s usually something like an invoice number, order ID, or transaction number — useful for reporting, but doesn’t have any descriptive attributes that need to be stored in a separate table.

"A degenerate dimension is a dimension key stored in the fact table that doesn't have a corresponding dimension table. It typically represents identifiers like invoice numbers or transaction IDs that are important for analysis, but don’t have additional attributes to justify a separate dimension."

- Periodic snapshot table - Monthly bill invoice for customer, bursting report will be generated, Transactional fact table is incorrect then periodic snapshot table will be incorrect.

  ![Screenshot 2025-04-14 at 6 52 22 PM](https://github.com/user-attachments/assets/2d0dfe4d-7a3e-4715-833e-77ffcdfca213)

  ![Screenshot 2025-04-14 at 6 56 40 PM](https://github.com/user-attachments/assets/e1ecf984-3cbe-48d5-b343-5e858f14520a)

  ![Screenshot 2025-04-14 at 6 57 17 PM](https://github.com/user-attachments/assets/96f1f3f1-5063-4db1-ba9d-4e93d218764a)

  ![Screenshot 2025-04-14 at 6 58 02 PM](https://github.com/user-attachments/assets/6e0f558a-6658-4795-8d20-ee2bf72cbd9b)

  ![Screenshot 2025-04-14 at 6 58 42 PM](https://github.com/user-attachments/assets/18cdc2f2-09b1-4b6a-9acb-d2e086c6b34a)

  ![Screenshot 2025-04-14 at 7 00 12 PM](https://github.com/user-attachments/assets/0c48341a-9392-4ae2-9f61-0fd32745da89)

  ![Screenshot 2025-04-14 at 7 01 43 PM](https://github.com/user-attachments/assets/d407989a-94f1-430f-948f-f805bc0d2c35)

  ![Screenshot 2025-04-14 at 7 02 12 PM](https://github.com/user-attachments/assets/d246a470-ee2d-40f4-9bfe-9121d0656978)

  ![Screenshot 2025-04-14 at 7 02 50 PM](https://github.com/user-attachments/assets/6fed5bd2-9fcc-46c6-9b54-2f1e18cc8092)

  ![Screenshot 2025-04-14 at 7 02 54 PM](https://github.com/user-attachments/assets/1e875cd8-0fe5-47b0-8be5-a0e5737b2f78)

  ![Screenshot 2025-04-14 at 7 04 15 PM](https://github.com/user-attachments/assets/80ab3af2-9d46-41d0-92f0-2c047302691f)

  ![Screenshot 2025-04-14 at 7 04 48 PM](https://github.com/user-attachments/assets/6e4b23d2-13a7-4985-90a5-f35ed6fb01ba)

  ![Screenshot 2025-04-14 at 7 05 17 PM](https://github.com/user-attachments/assets/4aabfe73-0e22-4b7e-823c-2826475dde10)

  ![Screenshot 2025-04-14 at 7 05 40 PM](https://github.com/user-attachments/assets/ab9ebd39-232e-4065-800c-548dc0e6616f)

  












