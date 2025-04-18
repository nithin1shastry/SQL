1. https://platform.stratascratch.com/coding/2004-number-of-comments-per-user-in-past-30-days?code_type=3
   
  ```
  SELECT user_id, COUNT(*) AS number_of_comments
  FROM fb_comments_count
  WHERE created_at BETWEEN DATE '2020-01-10' AND DATE '2020-02-10'
  GROUP BY user_id
  HAVING COUNT(*) > 0;
  ```

