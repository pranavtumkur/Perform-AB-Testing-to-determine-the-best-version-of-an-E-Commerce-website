--We are running an experiment at an item-level, which means all users who visit will see the same page, but the layout of different item pages may differ.
--View all data

SELECT 
  * 
FROM 
  dsv1069.final_assignments_qa
 
 
-- Use this table to compute order_binary for the 30 day window after the test_start_date for the test named item_test_2

SELECT
  test_assignment,
  COUNT(item_id) as items,
  SUM(order_binary_30d) AS ordered_items_30d
FROM
(
  SELECT 
   fa.test_assignment,
   fa.item_id, 
   MAX(CASE WHEN orders.created_at > fa.test_start_date THEN 1 ELSE 0 END)  AS order_binary_30d
  FROM 
    dsv1069.final_assignments fa
    
  LEFT OUTER JOIN
    dsv1069.orders
  ON 
    fa.item_id = orders.item_id 
  AND 
    orders.created_at >= fa.test_start_date
  AND 
    DATE_PART('day', orders.created_at - fa.test_start_date ) <= 30
  WHERE 
    fa.test_number= 'item_test_2'
  GROUP BY
    fa.test_assignment,
    fa.item_id
) item_level
GROUP BY test_assignment

-- Use this table to compute view_binary for the 30 day window after the test_start_date for the test named item_test_2

SELECT
test_assignment,
COUNT(item_id) AS items,
SUM(view_binary_30d) AS viewed_items,
SUM(views)/COUNT(item_id) AS average_views_per_item
FROM 
(
 SELECT 
   fa.test_assignment,
   fa.item_id, 
   MAX(CASE WHEN views.event_time > fa.test_start_date THEN 1 ELSE 0 END)  AS view_binary_30d,
   COUNT(views.event_id) AS views
  FROM 
    dsv1069.final_assignments fa
    
  LEFT OUTER JOIN 
    (
    SELECT 
      event_time,
      event_id,
      CAST(parameter_value AS INT) AS item_id
    FROM 
      dsv1069.events 
    WHERE 
      event_name = 'view_item'
    AND 
      parameter_name = 'item_id'
    ) views
  ON 
    fa.item_id = views.item_id
  AND 
    views.event_time >= fa.test_start_date
  AND 
    DATE_PART('day', views.event_time - fa.test_start_date ) <= 30
  WHERE 
    fa.test_number= 'item_test_2'
  GROUP BY
    fa.test_assignment,
    fa.item_id
) item_level
GROUP BY 
 test_assignment
 
 
--Use the https://thumbtack.github.io/abba/demo/abba.html to compute the lifts in metrics and the p-values for the binary metrics ( 30 day order binary and 30 day view binary) using a interval 95% confidence. 
