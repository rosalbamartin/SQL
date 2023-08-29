This is another SQL practice from the data with Danny program. This excersice consists in fix and debug the SQL codes which are all incorrect.
Danny has added his thoughts and also made some comments in the provided codes to identify some problem areas to facilitate the debuging of them.


# Danny’s Diner Syntax Solutions

### 1. What is the total amount each customer spent at the restaurant?
````sql
SELECT
  sales.customer_id,
  SUM(menu.price) AS total_sales
FROM dannys_diner.sales
INNER JOIN dannys_diner.menu
ON sales.product_id = menu.product_id
GROUP BY
  sales.customer_id
ORDER BY
  sales.customer_id;
````

### 2.How many days has each customer visited the restaurant?
````sql
 SELECT
  sales.customer_id,
  COUNT(DISTINCT order_date) AS count
  FROM dannys_diner.sales
  GROUP BY  sales.customer_id;
````

### 3. What was the first item(s) from the menu purchased by each customer?
````sql
  
WITH ordered_sales AS 
 (
  SELECT
    sales.customer_id,
    menu.product_name,
    sales.order_date,
    DENSE_RANK() OVER (
      PARTITION BY sales.customer_id
      ORDER BY sales.order_date
    ) AS order_rank
  FROM dannys_diner.sales
  INNER JOIN dannys_diner.menu
    ON sales.product_id = menu.product_id
)
SELECT 
  customer_id,
  product_name
FROM ordered_sales
WHERE order_rank = 1
GROUP BY customer_id, product_name;
````

### 4.What is the most purchased item on the menu and how many times was it purchased by all customers? OK ANSWER
````sql
SELECT
  menu.product_name,
  COUNT(sales.product_id) AS total_purchases
FROM dannys_diner.menu
JOIN dannys_diner.sales
  ON menu.product_id = sales.product_id
GROUP BY product_name
ORDER BY total_purchases DESC
LIMIT 1;
````
### 5.Which item(s) was the most popular for each customer?
````sql
WITH customer_cte AS
(
  SELECT
    sales.customer_id,
    menu.product_name,
    COUNT(menu.product_id) AS item_quantity,
    DENSE_RANK() OVER (PARTITION BY sales.customer_id
      ORDER BY COUNT(sales.customer_id)DESC) AS item_rank
  FROM dannys_diner.sales
  JOIN dannys_diner.menu
  ON sales.product_id = menu.product_id
  GROUP BY
    sales.customer_id,
    sales.product_id,
    menu.product_name
)
SELECT
  customer_id,
  product_name,
  item_quantity
FROM customer_cte
WHERE item_rank = 1;
````

### 6. Which item was purchased first by the customer after they became a member and what date was it? (including the date they joined)
````sql
WITH member_sales_cte AS
(
  SELECT
    sales.customer_id,
    sales.order_date,
    menu.product_name,
    DENSE_RANK() OVER (PARTITION BY sales.customer_id
      ORDER BY sales.order_date
    ) AS order_rank
  FROM dannys_diner.sales
  INNER JOIN dannys_diner.menu
    ON sales.product_id = menu.product_id
  INNER JOIN dannys_diner.members
    ON sales.customer_id = members.customer_id
  WHERE
    sales.order_date >= members.join_date::DATE
)
SELECT DISTINCT
  customer_id,
  order_date,
  product_name
FROM member_sales_cte
WHERE order_rank = 1;
````

### 7.Which menu item(s) was purchased just before the customer became a member and when?
````sql
WITH member_sales AS
(
  SELECT
    sales.customer_id,
    members.join_date,
    sales.order_date,
    menu.product_name,
   DENSE_RANK() OVER (PARTITION BY sales.customer_id
      ORDER BY sales.order_date DESC
    ) AS order_rank
  FROM dannys_diner.menu
  INNER JOIN dannys_diner.sales
    ON sales.product_id = menu.product_id
  INNER JOIN dannys_diner.members
    ON sales.customer_id = members.customer_id
  WHERE
    sales.order_date < members.join_date::DATE
)
SELECT
  customer_id,
  order_date,
  product_name
FROM member_sales
WHERE order_rank = 1;
````

### 8.What is the number of unique menu items and total amount spent for each member before they became a member?
````sql
SELECT
  sales.customer_id,
  COUNT(DISTINCT sales.product_id) AS unique_menu_items,
  SUM(menu.price) AS total_spend
FROM dannys_diner.sales
INNER JOIN dannys_diner.menu
  ON sales.product_id = menu.product_id
INNER JOIN dannys_diner.members
  ON sales.customer_id = members.customer_id
WHERE
  sales.order_date < members.join_date
GROUP BY sales.customer_id;
````
### 9. If each $1 spent equates to 10 points and sushi has a 2x points multiplier - how many points would each customer have?
````sql
SELECT
  sales.customer_id,
  SUM(CASE 
  WHEN menu.product_name = 'sushi' THEN  price * 10 * 2 
  ELSE price * 10  
  END) AS points
FROM dannys_diner.menu
inner JOIN dannys_diner.sales
ON sales.product_id = menu.product_id
GROUP BY customer_id
ORDER BY points DESC;
````
