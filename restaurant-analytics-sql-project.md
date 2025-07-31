# Restaurant Analytics SQL Project

## About This Project

The first objective is to explore the items on the menu. I worked with two tables: Menu Items and Order Details. I explored the first data set, Menu Items, to understand the restaurant's meals options.

## Objective A: Exploring Menu Items

### 1. View the Menu Items Table

```sql
USE restaurant_db;

-- 1. View the menu_items table.
SELECT *
FROM menu_items;
```

### 2. Find the Number of Items on the Menu

```sql
-- 2. Find the number of items on the menu.
SELECT COUNT(menu_item_id)
FROM menu_items;
```

**Result:**
| COUNT(menu_item_id) |
|---------------------|
| 32                  |

### 3. What are the Least and Most Expensive Items on the Menu?

```sql
-- 3. What are the least and the most expensive items on the menu?
SELECT *
FROM menu_items
ORDER BY menu_items.price;

SELECT *
FROM menu_items
ORDER BY menu_items.price DESC;
```

**Result - Most Expensive Items:**
| menu_item_id | item_name           | category | price |
|--------------|---------------------|----------|-------|
| 130          | Shrimp Scampi       | Italian  | 19.95 |
| 109          | Korean Beef Bowl    | Asian    | 17.95 |
| 110          | Pork Ramen          | Asian    | 17.95 |
| 125          | Spaghetti & Meatballs | Italian | 17.95 |
| 127          | Meat Lasagna        | Italian  | 17.95 |
| 131          | Chicken Parmesan    | Italian  | 17.95 |
| 132          | Eggplant Parmesan   | Italian  | 16.95 |
| 107          | Orange Chicken      | Asian    | 16.50 |

**Insight:** Edamame is the least expensive, costing $5.00, while Shrimp Scampi is the most expensive meal at $19.95.

### 4. How Many Italian Dishes are on the Menu?

```sql
-- 4. How many italian dishes are on the menu?
SELECT COUNT(*) AS num_italian_dishes
FROM menu_items
WHERE menu_items.category = 'Italian';
```

**Result:**
| num_italian_dishes |
|--------------------|
| 9                  |

**Insight:** There are 9 Italian dishes on the menu.

### 5. What are the Least and Most Expensive Italian Dishes?

```sql
-- 5. What are the least and most expensive Italian dishes on the menu?
SELECT *
FROM menu_items
WHERE menu_items.category = 'Italian'
ORDER BY menu_items.price;

SELECT *
FROM menu_items
WHERE menu_items.category = 'Italian'
ORDER BY menu_items.price DESC;
```

**Result - Italian Dishes by Price:**
| menu_item_id | item_name           | category | price |
|--------------|---------------------|----------|-------|
| 130          | Shrimp Scampi       | Italian  | 19.95 |
| 125          | Spaghetti & Meatballs | Italian | 17.95 |
| 127          | Meat Lasagna        | Italian  | 17.95 |
| 131          | Chicken Parmesan    | Italian  | 17.95 |
| 132          | Eggplant Parmesan   | Italian  | 16.95 |
| 128          | Cheese Lasagna      | Italian  | 15.50 |
| 129          | Mushroom Ravioli    | Italian  | 15.50 |
| 124          | Spaghetti           | Italian  | 14.50 |
| 126          | Fettuccine Alfredo  | Italian  | 14.50 |

**Insight:** Spaghetti is the least expensive Italian dish costing $14.50, while Shrimp Scampi is the most expensive costing $19.95.

### 6. How Many Dishes are in Each Category?

```sql
-- 6. How many dishes are in each category?
SELECT 
    menu_items.category,
    COUNT(menu_item_id) AS num_dishes
FROM menu_items
GROUP BY menu_items.category;
```

**Result:**
| category | num_dishes |
|----------|------------|
| American | 6          |
| Asian    | 8          |
| Mexican  | 9          |
| Italian  | 9          |

**Insight:** There are 6 American, 8 Asian, 9 Italian, and 9 Mexican dishes in each category.

### 7. What are the Average Dish Prices for Each Category?

```sql
-- 7. What is the average price within each category?
SELECT 
    menu_items.category,
    AVG(menu_items.price) AS avg_price
FROM menu_items
GROUP BY menu_items.category;
```

**Result:**
| category | avg_price |
|----------|-----------|
| American | 10.066667 |
| Asian    | 13.475000 |
| Mexican  | 11.800000 |
| Italian  | 16.750000 |

**Insight:** The average dish price for American is $10.07, Asian $13.48, Italian $16.75, and Mexican $11.80.

## Objective B: Exploring Order Details

I explored the second data set, order_details, to understand the customer's choices and order history.

### 8. View the Order Details Table

```sql
-- 8. View the order_details table.
SELECT *
FROM order_details;
```

### 9. What is the Date Range of the Table?

```sql
-- 9. What is the date range of the table?
SELECT 
    MIN(order_details.order_date) AS start_range,
    MAX(order_details.order_date) AS end_range
FROM order_details;
```

**Result:**
| start_range | end_range  |
|-------------|------------|
| 2023-01-01  | 2023-03-31 |

**Insight:** The dataset occurs in a period of 3 months and the date ranges from 2023-01-01 to 2023-03-31.

### 10. How Many Orders Were Made Within This Date Range?

```sql
-- 10. How many orders were made in this date range?
SELECT COUNT(DISTINCT order_details.order_id) AS num_orders
FROM order_details;
```

**Result:**
| num_orders |
|------------|
| 5370       |

**Insight:** 5,370 orders were made in the past three months.

### 11. How Many Items Were Ordered Within This Date Range?

```sql
-- 11. How many items were ordered in this date range?
SELECT COUNT(*) AS num_items
FROM order_details;
```

**Result:**
| num_items |
|-----------|
| 12234     |

**Insight:** 12,234 items were purchased by customers in the past three months.

### 12. Which Orders Had the Most Number of Items?

```sql
-- 12. Which orders had the most number of items?
SELECT 
    order_details.order_id,
    COUNT(order_details.item_id) AS num_items
FROM order_details
GROUP BY order_details.order_id
ORDER BY num_items DESC;
```

**Insight:** 7 different customers ordered a total of 14 items from the menu.

### 13. How Many Orders Had More Than 12 Items?

```sql
-- 13. How many orders had more than 12 items?
SELECT COUNT(*)
FROM (
    SELECT 
        order_details.order_id,
        COUNT(order_details.item_id) AS num_items
    FROM order_details
    GROUP BY order_details.order_id
    HAVING num_items > 12
) AS num_orders;
```

**Insight:** 20 people ordered more than 12 items from the menu.

## Objective C: Combined Analysis

I combined the menu_items and order_details tables into a single table to get more information about the customers orders.

### 14. Combine the Menu Items and Order Details Tables

```sql
-- 14. Combine the menu_items and order_details tables into a single table.
SELECT *
FROM order_details od
LEFT JOIN menu_items mi
ON od.item_id = mi.menu_item_id;
```

### 15. What Were the Least and Most Ordered Items? What Categories Were They In?

```sql
-- 15. What are the least and most ordered items? What categories were they in?
SELECT 
    mi.item_name,
    mi.category,
    COUNT(order_details_id) AS num_purchases
FROM order_details od
LEFT JOIN menu_items mi
ON od.item_id = mi.menu_item_id
GROUP BY 
    mi.item_name,
    mi.category
ORDER BY num_purchases DESC;
```

**Insight:** Chicken Tacos and Hamburger were the least and most ordered, respectively. Chicken Tacos is in the Mexican category and Hamburger is in the American category.

### 16. What Were the Top 5 Orders That Spent the Most Money?

```sql
-- 16. What were the top 5 orders that spent the most money?
SELECT 
    order_id,
    SUM(mi.price) AS total_spend
FROM order_details od
LEFT JOIN menu_items mi
ON od.item_id = mi.menu_item_id
GROUP BY order_id
ORDER BY total_spend DESC
LIMIT 5;
```

**Insight:** Customers with the order ID (440, 2075, 1957, 330, 2675) spent a total of $948.10.

### 17. View the Details of the Highest Spend Order

```sql
-- 17. View the details of the highest spend order. What insights can you gather from the results?
SELECT 
    category,
    COUNT(item_id) AS num_items
FROM order_details od
LEFT JOIN menu_items mi
ON od.item_id = mi.menu_item_id
WHERE od.order_id = 440
GROUP BY category;
```

**Insight:** The categories of the top items bought are 2 American, 2 Asian, 8 Italian and 2 Mexican. The top customers spend most on Italian dishes.

### 18. View the Details of the Top 5 Highest Spend Orders

```sql
-- 18. View the details of the top 5 highest spend order. What insights can you gather from the results?
SELECT 
    order_id,
    category,
    COUNT(item_id) AS num_items
FROM order_details od
LEFT JOIN menu_items mi
ON od.item_id = mi.menu_item_id
WHERE od.order_id IN (440, 2075, 1957, 330, 2675)
GROUP BY 
    order_id,
    category;
```

**Insight:** The highest spend orders tend to spend a lot on Italian food. We should keep the expensive Italian dishes on the menu because people seem to be ordering them a lot.

