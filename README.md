# K means cluster plot segmenting customers into three groups based on RFM scores as part of iO-Sphere data training course.

RFM scores calculated using SQL code:

SELECT *,
  CASE
    WHEN latest_purchase_date >= '2022-06-01' AND latest_purchase_date <= DATE_ADD('2022-06-01', INTERVAL 19 DAY) THEN 1
    WHEN latest_purchase_date > DATE_ADD('2022-06-01', INTERVAL 19 DAY) AND latest_purchase_date <= DATE_ADD('2022-06-01', INTERVAL 37 DAY) THEN 2
    WHEN latest_purchase_date > DATE_ADD('2022-06-01', INTERVAL 37 DAY) AND latest_purchase_date <= DATE_ADD('2022-06-01', INTERVAL 56 DAY) THEN 3
    WHEN latest_purchase_date > DATE_ADD('2022-06-01', INTERVAL 56 DAY) AND latest_purchase_date <= DATE_ADD('2022-06-01', INTERVAL 74 DAY) THEN 4
    WHEN latest_purchase_date > DATE_ADD('2022-06-01', INTERVAL 74 DAY) AND latest_purchase_date <= DATE_ADD('2022-06-01', INTERVAL 93 DAY) THEN 5
    WHEN latest_purchase_date > DATE_ADD('2022-06-01', INTERVAL 93 DAY) AND latest_purchase_date <= DATE_ADD('2022-06-01', INTERVAL 111 DAY) THEN 6
    WHEN latest_purchase_date > DATE_ADD('2022-06-01', INTERVAL 111 DAY) AND latest_purchase_date <= DATE_ADD('2022-06-01', INTERVAL 130 DAY) THEN 7
    WHEN latest_purchase_date > DATE_ADD('2022-06-01', INTERVAL 130 DAY) AND latest_purchase_date <= DATE_ADD('2022-06-01', INTERVAL 148 DAY) THEN 8
    WHEN latest_purchase_date > DATE_ADD('2022-06-01', INTERVAL 148 DAY) AND latest_purchase_date <= DATE_ADD('2022-06-01', INTERVAL 167 DAY) THEN 9
    WHEN latest_purchase_date > DATE_ADD('2022-06-01', INTERVAL 167 DAY) THEN 10
  END AS Recency,
NTILE(10) OVER(ORDER BY LOG(transaction_count)) AS Frequency,
NTILE(10) OVER(ORDER BY LOG(total_revenue)) AS Monetary
  FROM `prism-2023-c1.Prism_Main.users`
  WHERE transaction_count > 0
  AND latest_purchase_date >= '2022-06-01';
