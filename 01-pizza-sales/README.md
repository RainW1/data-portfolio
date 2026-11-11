# Lunch and dinner peaks drive 48% of a pizza shop's revenue

*Practice project using public data. The client brief is simulated.*

**Live dashboard:** [View dashboard](https://datastudio.google.com/reporting/a6366484-ed43-4d30-8ea7-6362423033ec)
**Tools:** Google Sheets, Looker Studio

<img width="900" alt="Dashboard" src="https://github.com/user-attachments/assets/b8f2507c-dc1e-4dc8-a9db-b8b861a9514f" />

## Brief
A small pizza shop owner wants to know which hours, days and pizzas bring in the most money, so they can plan staff and promos better.

## Data
- Source: [Pizza Place Sales, Maven Analytics](https://mavenanalytics.io/data-playground/pizza-place-sales)
- 4 tables: orders (21,350), order_details (48,620 rows), pizzas, pizza_types (32 pizzas in 4 categories)
- Covers all of 2015
- The source data was already clean: no blanks and no duplicate IDs. Most of the work was joining the 4 tables and checking the results.

Things I found while checking:
- Only 358 of 365 days have orders, so 7 days are missing (not investigated yet)
- One product has an odd name: "The Vegetables + Vegetables Pizza"
- Brie Carre is only sold in Small, at almost double the price of other Smalls

## Process
1. Imported the 4 CSV files into Google Sheets
2. Added hour and weekday columns from the order date and time
3. Joined price, pizza name and category into order_details with XLOOKUP
4. Added revenue (quantity x price) and checked the totals against the source
5. Built pivots for revenue by hour, weekday, category and pizza
6. Built a one-page dashboard in Looker Studio

**A decision I made:** I counted orders using unique order_id, not rows. One order can have several pizza lines, so counting rows would make the average order value $16.82 instead of the correct $38.31.

**Bugs I caught in my own work:**
- My lookup ranges shifted when I copied the formula down, which caused missing prices. Fixed it by locking the ranges.
- Autofill stopped at row 33,035, which left 32% of revenue with no weekday. Fixed it and added blank and error checks.

## Results

**1. Peak hours**
Lunch (12:00 to 14:00) and dinner (17:00 to 19:00) bring in 48.1% of total revenue.
Recommendation: add 1 or 2 shift staff only around these peaks, so the kitchen keeps up without paying for idle hours.

**2. Weekdays**
Thursday to Saturday bring in 46.8% of revenue, only a little above the 42.9% you would get if every day were equal. Friday is the best day ($136K), 37% above Sunday ($99K).
Recommendation: the weekly pattern is mild, so plan staff by hour first. Test a Sunday family bundle for 4 weeks.

**3. Chicken pizzas**
Chicken has the fewest pizzas (6) but earns the most per pizza, about $32.7K each compared with $21.5K for Veggie. The top 3 pizzas by revenue are all chicken.
Recommendation: test 1 or 2 new chicken pizzas and feature chicken in promos.

**4. Brie Carre**
It is the lowest earning pizza (1.4% of revenue). It only comes in Small and costs $23.65, almost double other Smalls.
Recommendation: test a lower price for 4 weeks. If sales do not improve, take it off the menu.

## Effort
- Time: about 4 hours
- What I would charge: $35 (cleaning plus a one-page dashboard)
