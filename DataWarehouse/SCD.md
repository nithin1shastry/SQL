# SCD with real example
- SCD change over time and no fixed pattern associated with that
- Price of product won't change over time in a day. Whereas stock data can change in few seconds

## Standard SCD
- SCD 0
  - If change in source system, we won't implement it in warehouse table.
  - Fax number is changed in source but we won't change in warehouse table as its outdated and irrelevant and we reject it.

    ![Screenshot 2025-04-14 at 7 31 35 PM](https://github.com/user-attachments/assets/6d0de973-6a86-435e-aefa-89e95ddb8061)

- SCD 1
  - We maintain latest snapshot of data, and not history
  - customer address, no history of customers adddress is stored
  - Initially a employee was assinged to dev but he is lead. Then we update to lead. Only lead is captured. No prev value is captured.

    ![Screenshot 2025-04-14 at 7 32 58 PM](https://github.com/user-attachments/assets/f13e9518-a77c-4a12-bf36-5addeb015b35)

    ![Screenshot 2025-04-14 at 7 33 05 PM](https://github.com/user-attachments/assets/013ae519-865a-416d-83ae-01322164d96e)

- SCD 2
  - Every time there is change in source dim table, we will add additional row in warehouse table



