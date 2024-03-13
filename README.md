# Wunmi's portfolio

## 30days SQL Challenge

This challenge was organized by Techavilly to help upcoming data Analyst in their Data analytics journey. We worked with different datasets which will be shared below with their respective questions and queries.

### Links to the Datasets
- [Runners](https://techavilly.net/wp-content/uploads/2023/10/runners.xlsx)
- [Customer orders](https://techavilly.net/wp-content/uploads/2023/10/customer_orders.xlsx)
- [Runner orders](https://techavilly.net/wp-content/uploads/2023/10/runner_orders.xlsx)
- [Pizza names](https://techavilly.net/wp-content/uploads/2023/10/pizza_names.xlsx)
- [Pizza recipe](https://techavilly.net/wp-content/uploads/2023/10/pizza_recipe.xlsx)
- [Pizza toppings](https://techavilly.net/wp-content/uploads/2023/10/pizza_toppings-.xlsx)
- [Movie Data - Movie Data](https://techavilly.net/wp-content/uploads/2023/03/Movie-Data.zip)
- [Sample Superstore Data - Sample Superstore](https://techavilly.net/wp-content/uploads/2023/04/Sample-Superstore-Complete.xlsx)
- [Bonus table(link to download)](https://yvzdlz.clicks.mlsend.com/te/cl/eyJ2Ijoie1wiYVwiOjM0NTkxOCxcImxcIjoxMDI1OTE0NjU3NzU5NTcxMzAsXCJyXCI6MTAyNTkxNDY5NTg4NTc5NTI0fSIsInMiOiI3N2ExMjhjYTNiMmE0OTVlIn0)
- [Share Price data](https://techavilly.net/wp-content/uploads/2023/10/SharePrice-.xlsx)
- [Employee Table](https://techavilly.net/wp-content/uploads/2023/10/Employee-Table.xlsx)

### Tools
Mysql Server [Download here](https://dev.mysql.com/downloads/windows/installer/8.0.html)

### Questions and Outputs

**Day 1 Question**: Using the movie Data, write a query to show the titles and movie released in 2017 whose vote count is more than 15 and runtime is more than 100.

#### Output
```sql
--title where release year is 2017, vote count > 15 and runtime > 100
select original_title from Movie_data
where release_date between '2017-01-01' and '2017-12-31'
and vote_count > 15 and runtime > 100;
```
![image](https://github.com/oenijesiku/Wunmi_portfolio/assets/87021092/6fe0451f-d7a6-41ba-b29d-e57909e27a6a)

**Day 2 Question**: Using the pizza Data, write a query to show how many pizzas were ordered.
#### Output
```sql
--The count of the all customer's(pizza) order
select count(*) as total_pizza_ordered from customer_orders
```
![image](https://github.com/oenijesiku/Wunmi_portfolio/assets/87021092/592e4f4c-0225-432f-8cf3-a2567cc4b73e)

**Day 3 Question**: 



























