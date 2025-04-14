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

    ![Screenshot 2025-04-14 at 7 38 19 PM](https://github.com/user-attachments/assets/0dc0476e-d403-4df4-bd56-049e8cb6dd99)

    ![Screenshot 2025-04-14 at 7 38 36 PM](https://github.com/user-attachments/assets/18bf9c78-ab41-4143-b2c9-4981137cbb6a)

    ![Screenshot 2025-04-14 at 7 39 28 PM](https://github.com/user-attachments/assets/3731d5fa-6e4f-41f4-92cf-e3d2766eb026)

- SCD 3
  - Every time there is change in source dim table, we will add additional column in warehouse table
 
  ![Screenshot 2025-04-14 at 7 42 50 PM](https://github.com/user-attachments/assets/97923545-cc0e-469a-9fc0-3f364b058c52)

  ![Screenshot 2025-04-14 at 7 43 04 PM](https://github.com/user-attachments/assets/4e00f2f0-3496-4b93-8287-fd85e29717d5)

  ![Screenshot 2025-04-14 at 7 43 17 PM](https://github.com/user-attachments/assets/89cc46d9-05a1-48c0-b03f-894d500f442a)

- SCD 4
  - History Table
  - Mix of SCD 1 + SCD 2
  - SCD 2 maintained in history table
  - SCD 1 maintained in different table which has latest snapshot
  - Eg - Investment banking -> bit coin rapidly changes, trade happpens on latest data
 
    ![Screenshot 2025-04-14 at 7 45 04 PM](https://github.com/user-attachments/assets/0a8946dd-65a6-495a-9b0f-793ff5d26ecc)

    ![Screenshot 2025-04-14 at 7 45 16 PM](https://github.com/user-attachments/assets/92786793-9782-46b2-b81e-ec49c01931bd)

- SCD 6
  - SCD 1 + 2 + 3
    
    ![Screenshot 2025-04-14 at 7 49 22 PM](https://github.com/user-attachments/assets/c4c89957-dc71-448c-855d-4c77106defc0)

    ![Screenshot 2025-04-14 at 7 49 29 PM](https://github.com/user-attachments/assets/3c3e305c-2b08-4b25-92c3-9bc011172ff8)

    ![Screenshot 2025-04-14 at 7 49 46 PM](https://github.com/user-attachments/assets/edced6aa-6191-4368-a097-36940b20c9e0)


     ![Screenshot 2025-04-14 at 7 50 15 PM](https://github.com/user-attachments/assets/be8c4984-6214-4b47-89a7-7e6a536ce4ff)

    







  









