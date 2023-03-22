# RFM_Cluster_Plot

From customer user data, where RFM scores are calculated with the SQL code:

SELECT *,
  CASE 
    WHEN latest_purchase_date >= '2022-01-01' AND latest_purchase_date <= DATE_ADD('2022-01-01', INTERVAL 37 DAY) THEN 1
    WHEN latest_purchase_date > DATE_ADD('2022-01-01', INTERVAL 37 DAY) AND latest_purchase_date <= DATE_ADD('2022-01-01', INTERVAL 73 DAY) THEN 2
    WHEN latest_purchase_date > DATE_ADD('2022-01-01', INTERVAL 73 DAY) AND latest_purchase_date <= DATE_ADD('2022-01-01', INTERVAL 110 DAY) THEN 3
    WHEN latest_purchase_date > DATE_ADD('2022-01-01', INTERVAL 110 DAY) AND latest_purchase_date <= DATE_ADD('2022-01-01', INTERVAL 146 DAY) THEN 4
    WHEN latest_purchase_date > DATE_ADD('2022-01-01', INTERVAL 146 DAY) AND latest_purchase_date <= DATE_ADD('2022-01-01', INTERVAL 183 DAY) THEN 5
    WHEN latest_purchase_date > DATE_ADD('2022-01-01', INTERVAL 183 DAY) AND latest_purchase_date <= DATE_ADD('2022-01-01', INTERVAL 219 DAY) THEN 6
    WHEN latest_purchase_date > DATE_ADD('2022-01-01', INTERVAL 219 DAY) AND latest_purchase_date <= DATE_ADD('2022-01-01', INTERVAL 256 DAY) THEN 7
   WHEN latest_purchase_date > DATE_ADD('2022-01-01', INTERVAL 256 DAY) AND latest_purchase_date <= DATE_ADD('2022-01-01', INTERVAL 292 DAY) THEN 8
    WHEN latest_purchase_date > DATE_ADD('2022-01-01', INTERVAL 292 DAY) AND latest_purchase_date <= DATE_ADD('2022-01-01', INTERVAL 329 DAY) THEN 9
    WHEN latest_purchase_date > DATE_ADD('2022-01-01', INTERVAL 329 DAY) AND latest_purchase_date <= DATE_ADD('2022-01-01', INTERVAL 365 DAY) THEN 10
  END AS Recency,
NTILE(10) OVER(ORDER BY LOG(transaction_count)) AS Frequency,
NTILE(10) OVER(ORDER BY LOG(total_revenue)) AS Monetary
  FROM `prism-2023-c1.Prism_Main.users`
  WHERE transaction_count > 0 
  AND latest_purchase_date >= '2022-01-01';
