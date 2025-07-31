# Restaurant Menu Performance Analysis

A small restaurant is seeking to better understand its menu performance since they debuted a new menu at the start of the year. We will dig into the customer data to see which menu items are doing well / not well and what the top customers seem to like best.

## Objective 1: Explore the items table

Get a better understanding of the items table by finding:

- The number of items on the menu, and the least and most expensive items
- How many Italian dishes are on the menu and what is the price range?
- How many dishes are in each category? What is the average dish price within each category?

## Objective 2: Explore the orders table

Get a better understanding of the orders table by finding:

- The date range
- Number of items within each order
- Which orders had the most number of items?
- How many orders had more than 12 items?

## Objective 3: Analyze customer behavior

Combine order_details and menu_items tables together to answer:

- What were the least and most ordered items? What categories were they in?
- Where were the top 5 orders that spent the most money?
- Which specific items were purchased from the highest spending orders?

## Key Insights

**Popular Items:** Italian dishes like Spaghetti & Meatballs, Meat Lasagna, and Eggplant Parmesan consistently appeared in the highest-grossing and most-ordered categories. This suggests a strong preference for Italian cuisine among customers.

**Profitable Orders:** The highest-grossing order contained a mix of American and Italian dishes, highlighting the appeal of cross-category variety.

**Menu Diversification:** Asian and Mexican categories also demonstrated moderate popularity with items like Tofu Pad Thai and Chicken Burrito, appealing to niche customer segments.

## Recommendations

**Expand Italian Offerings:** Given the consistent popularity of Italian dishes, the restaurant should consider expanding its Italian menu, introducing seasonal variations, or promotional offers for these items.

**Combo Deals:** Create cross-category combo meals featuring popular dishes from Italian, American, and Asian cuisines to boost order value and cater to diverse preferences.

**Optimize Marketing:** Highlight Italian dishes in marketing campaigns and dining promotions to attract more patrons and drive sales.

**Customer Feedback:** Solicit direct customer feedback to identify opportunities to refine or add new menu items.

## Technologies Used

- **Database:** MySQL
- **Analysis Tools:** SQL queries for data exploration and analysis
- **Data Sets:** 
  - `menu_items` table (32 items across 4 categories)
  - `order_details` table (12,234 orders over 3 months)

## Database Schema

The project uses two main tables:
- **menu_items**: Contains menu item details (ID, name, category, price)
- **order_details**: Contains order information (order ID, item ID, order date)

---

*This analysis provides valuable insights into customer preferences and can guide menu optimization and marketing strategies for the restaurant.*
