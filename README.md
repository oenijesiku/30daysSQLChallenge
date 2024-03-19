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
#### Query
```sql
--title where release year is 2017, vote count > 15 and runtime > 100
select original_title from Movie_data
where release_date between '2017-01-01' and '2017-12-31'
and vote_count > 15 and runtime > 100;
```
![image](https://github.com/oenijesiku/Wunmi_portfolio/assets/87021092/6fe0451f-d7a6-41ba-b29d-e57909e27a6a)

**Day 2 Question**: Using the pizza Data, write a query to show how many pizzas were ordered.
#### Query
```sql
--The count of the all customer's(pizza) order
select count(*) as total_pizza_ordered from customer_orders
```
![image](https://github.com/oenijesiku/Wunmi_portfolio/assets/87021092/592e4f4c-0225-432f-8cf3-a2567cc4b73e)

**Day 3 Question**: Using the Pizza Data, write a query to show How many successful orders were delived by each runner?
#### Query
```sql
--Select runner_id and count for all record with an alias
select runner_id, count(*) as number_of_successful_order from runner_orders

--To get the number of successful order, we filter using the where clause
where pickup_time is not null 
	and cancellation is null
	
--We proceed to group by runner_id since we need an aggregate
group by runner_id
```
![image](https://github.com/oenijesiku/Wunmi_portfolio/assets/87021092/669f4df4-a7e4-4af3-b162-134da633c0e0)

To get the number of successful orders, I filtered using pickup time and cancellation. I added cancellation as a condition because the pizza might have been picked up and canceled by a customer if delivery was delayed.

**Day 4 Question**: Write a query to show the top 10 movie titles whose language is English and French and the budget is more than 1,000,000.
#### Query
```sql
--select the first 10 original title and alias as title
select top 10 original_title as title

--from the movie data set
from movie_data

--filter the language column using the where clause for English and French
where original_language in ('en','fr')

--use the and command in conjunction with the where clause to filter for budget above 1 million
and budget > '1,000,000'
```
![image](https://github.com/oenijesiku/Wunmi_portfolio/assets/87021092/2b585446-e797-4fe3-b720-f64c73011e41)

**Day 5 Question**: Using the Pizza Data, Write a query to show the number of each type of pizza was delivered.
#### Query
```sql
-- select pizza name and its count alias as pizza_deliveries 
select pizza_name, count(pizza_name) as pizza_deliveries

--write a join statement to combine pizza name, customers order and runners order in a table
from pizza_names as pn
join customer_orders as co
on pn.pizza_id = co.pizza_id
join runner_orders as ro
on co.order_id = ro.order_id

--Filter using the where statement
where cancellation is null

--Group by pizza_name for an aggregate for each pizza name
group by pizza_name
```
![image](https://github.com/oenijesiku/Wunmi_portfolio/assets/87021092/7477e748-b8c5-400d-a924-484b2daf3a39)

**Day 6 Question**: The Briggs company wants to ship some of their products to customers in selected cities but they want to know the average days it'll take to deliver those items to Dallas, Los Angeles, Seattle and Madison. Using Sample Superstore data, write a query to show the average delivery days to those cities. Only show the City and Average delivery days columns in your output.
#### Query
```sql
--Select city and calculate the average delivery days
select city, avg(datediff(day, Order_Date, Ship_Date)) as avg_delivery_days

--From the Sample superstore dataset
from Sample_Superstore_Complete

--filter for the required countries
where City in ('Dallas', 'Los Angeles','Seattle','Madison')

--Group by city
group by city
```
![image](https://github.com/oenijesiku/Wunmi_portfolio/assets/87021092/1d7027bf-a59a-4778-b1fc-5a18eb40a2d4)

**Day 8 Question**: It's getting to the end of the year and The Briggs Company wants to reward the customer who made the highest sales ever. Using the Sample Super Store, write a query to help the company identify this customer and category of business driving the sales. Let your output show the customer Name, the Category and the total sales. Round the total sales to the nearest whole number.
#### Query
```sql
--Select the customer and category with the highest sales as an integer
select top 1 Customer_Name, category, cast(sum(Sales) as integer) as total_sales

--from the Sample Superstore dataset
from Sample_Superstore_Complete

--Group by Customer name and category
group by Customer_Name, category

--Order by total_sales
order by total_sales desc
```
![image](https://github.com/oenijesiku/Wunmi_portfolio/assets/87021092/2fd79050-1bb9-4f1c-8912-21955fc21c02)

**Day 9 Question**: The Briggs Company has 3 categories of business generating revenue for the company. They want to know which of them is driving the business. Write a query to show the total sales and percentage contribution by each category. Show Category, Total Sales and Percentage contribution columns in your output.
#### Query
```sql
select category, 
		sum(sales) as total_sales, 
		(sum(sales)/(select sum(sales)from Sample_Superstore_Complete)) *100 as perc_contribution
from Sample_Superstore_Complete
group by category
order by perc_contribution desc
```
![image](https://github.com/oenijesiku/Wunmi_portfolio/assets/87021092/3672208c-85ef-41c2-a3a7-d086daf7c491)

**Day 10 Question**: After seeing the Sales by Category, the Briggs company became curious and wanted to dig deeper to see which subcategory is selling the most. They need the help of an analyst. Please help the company to write a query to show the sub category and the Total sales of each sub category. Let your query display only the Subcategory and the Total sales columns to see which product sells the most.
#### Query
```sql
--Select the sub-category and total sales
select Sub_category, round(sum(Sales), 2) as total_sales

--from the Sample Superstore dataset
from Sample_Superstore_Complete

--Group by sub-category
group by Sub_category

--Order by total_sales
order by total_sales desc
```
![image](https://github.com/oenijesiku/Wunmi_portfolio/assets/87021092/123cd6a3-bade-4f44-bdcf-11fb7d16f91a)

**Day 11 Question**: Now that you've identified phones as the business driver in terms of revenue. The company wants to know the total "phones sales" by year to understand how "each year" performed. As the Analyst, please help them to show the breakdown of the total sales by year in descending order. Let your output show only Total sales and Sales year column.
#### Query
```sql
--select year from order date and sum of sales rounding up to 2D.P
select year (order_date) as Sales year, round(sum (Sales), 2) as Total_sales

--from the required dataset
from Sample_Superstore_Complete

--filter the sub category for phones
where Sub Category "Phones"

--group by year from order date
group by year(order_date)

--order by total sales
order by Total_sales desc
```
![image](https://github.com/oenijesiku/Wunmi_portfolio/assets/87021092/5bfb0d09-2dc4-417a-a5f9-b77c12fd06cd)

**Day 12 Question**: The Director of Analytics has requested a detailed analysis of the Briggs Company. To fulfill this request, he needs you to generate a table that displays the profit margin of "each segment". The table should include the segments, total sales, total profit and the profit margin. To ensure accuracy, the profit margin should be arranged in descending order.
#### Query
```sql
--select segment, sum of sales, profit and a calculation for profit margin rounding up to 2D.P
select Segment,
		round(sum(Sales), 2) as Total_sales, 
		round(sum(Profit), 2) as Total_profit, 
		round((sum(Profit)/sum(Sales) * 100), 2) as Profit_margin

--from the required dataset
from Sample_Superstore_Complete

--group by segment
group by Segment

--order by profit_margin
order by Profit_margin desc
```
![image](https://github.com/oenijesiku/Wunmi_portfolio/assets/87021092/ba3f983e-b5da-49ec-989f-564cab932a18)

**Day 13 Question**: As we conclude the analysis for The Briggs Company, they got some reviews on their website regarding their new product. Please use the Bonus table to write a query that returns only the meaningful reviews. These are reviews that are readable in English. There are two columns in the table, let your output return only the review column.
#### Query
```sql
--select review
select Review

--from the bonus table
from BonusTable1

--filter translation as null
where translation is null
```
![image](https://github.com/oenijesiku/Wunmi_portfolio/assets/87021092/e8f4b905-6f34-4986-83ad-5ca52268103d)

**Day 15 Question**: Your company started consulting for Micro Bank who needs to analyze their marketing data to understand their customers better. This will help them plan their next marketing campaign. You are brought on board as the analyst for this job. They have an offer for customers who are divorced but they need data to back up the campaign. Using the marketing data, write a query to show the percentage of customers who are divorced and have balances greater than 2000
#### Query
```sql
--select the percentage of total customers and alias as perc_divorced_with_high_bal
select (count(*) * 100/(select count(*) from [Marketing Data])) as perc_divorced_with_high_bal

--from the marketing dataset
from [Marketing Data]

--filter marital for divorced and balances > 2000
where marital = 'divorced' and balance > 2000;
```
![image](https://github.com/oenijesiku/Wunmi_portfolio/assets/87021092/06b5d433-3545-4c5c-ad23-b167ecdd6e1a)

**Day 16 Question**: Micro Bank wants to be sure they have enough data for this campaign and would like to see the total count of each job as contained in the dataset. Using the marketing data, write a query to show the count of each job, arrange the total count in Desc order.
#### Query
```sql
--select job and its count
select job, count(*) as job_count

--from the required dataset
from [Marketing Data]

--group by job
group by job

--order by the count of job
order by job_count desc; 
```
![image](https://github.com/oenijesiku/Wunmi_portfolio/assets/87021092/74bd4afa-21f4-4aba-8b49-e11eb008b208)

**Day 17 Question**: Just for clarity purposes, your company wants to see which education level got to the management job the most. Using the marketing data, write a query to show the education level that gets the management position the most. Let your output show the education, job and the count of jobs columns.
#### Query
```sql
--select the top 1 educational level, job and job count
select top 1 education, job, count(job) as job_count

--from the required dataset
from [Marketing Data]

--filter management from the job column
where job='management'

--group by education and job
group by education,job

--order by job count
order by job_count desc;
```
![image](https://github.com/oenijesiku/Wunmi_portfolio/assets/87021092/14ab68f9-f078-4b1a-975b-a153ba5f899a)

**Day 18 Question**: Write a query to show the average duration of customers' employment in management positions. The duration should be calculated in years.
#### Query
```sql
--select the average of dration dividing by 52 weeks
select avg(duration)/52 as avg_employment_duration

--from the marketing dataset
from [Marketing Data]

--filter management on the job column
where job = 'management'
```
![image](https://github.com/oenijesiku/Wunmi_portfolio/assets/87021092/30d03436-319d-4fc0-836e-4591fbda1a63)

**Day 19 Question**: What's the total number of customers that have housing, loan and are single?
#### Query
```sql
--select loan, housing, marital and total count of customers
select loan, housing, marital, count(*) as total_count

--from the marketing data
from [Marketing Data]

--filter loan and housing as yes and marital status as single
where loan = 'yes' 
		and housing ='yes'
		and marital ='single'

--group by loan, housing and marital status
group by loan, housing, marital;
```
![image](https://github.com/oenijesiku/Wunmi_portfolio/assets/87021092/63c6b189-2458-4e56-9637-2903b6bb701a)

**Day 20 Question**: Using the Movie data, write a query to show the movie title with runtime of at least 250. Show the title and runtime columns in your output.
#### Query
```sql
--select title and runtime
select title, runtime

--from the movie dataset
from Movie_data

--filter runtime to be greater or equal to 250
where runtime  >= 250

--order in desc
order by runtime desc
```
![image](https://github.com/oenijesiku/Wunmi_portfolio/assets/87021092/ecd3de57-7faa-4f15-b59c-ef1ba9cddec3)

**Day 22 Question**: Using the Employee Table dataset, write a query to show all the employees first name and last name and their respective salaries. Also, show the overall average salary of the company and calculate the difference between each employee's salary and the company average salary.
#### Query
```sql
--write a query to show first name, last name, salary, overall avg salary of the company and 
--diff btw each employee and company avg salary
select first_name, last_name, salary, avg(salary) over() as com_avg_salary, salary-avg(salary) over() as salary_diff
from Employee_Table
```
![image](https://github.com/oenijesiku/Wunmi_portfolio/assets/87021092/c114596c-31d6-4efa-b633-cee4a9f459a1)

**Day 23 Question**: Using the Share Price dataset, write a query to show a table that displays the highest daily decrease and the highest daily increase in share price.
#### Query
```sql
--write a query to show a table that displays the highest daily decrease and the highest daily increase
select round(min([close]-[open]),2) as highest_daily_decrease, 
	round(max([close]-[open]), 2) as highest_daily_increase
from SharePrice
```
![image](https://github.com/oenijesiku/Wunmi_portfolio/assets/87021092/c86ab052-25e3-47a1-8c32-4a960df45851)

**Day 24 Question**: Our client is planning their logistics for 2024, they want to know the average number of days it takes to ship to the top 10 states. Using the sample superstore dataset, write a query to show the state and the average number of days between the order date and the ship date to the top 10 states
#### Query
```sql
--select state and calculate the average delivery days
select top 10 [State], avg(datediff(day, Order_Date, Ship_Date)) as AvgDaysBtwOrderAndShip

--from the Sample superstore dataset
from Sample_Superstore_Complete

--group by state
group by [state]

--order by the average delivery days 
order by avg(datediff(day, Order_Date, Ship_Date))
```
![image](https://github.com/oenijesiku/Wunmi_portfolio/assets/87021092/fddd50de-d894-499e-8a8c-7cc00bf6314e)

**Day 25 Question**: Your company received a lot of bad reviews about some of your products lately and the management wants to see which products they are and how many have been returned so far. Using the Orders and returns table, write a query to see the top 5 most returned products from the company.
#### Query
```sql
--select the first 5 product name, id and total count aliasing as product count
select top 5 Product_Name, Product_ID, count(*) as product_count

--from the order dataset aliasing as o to enable joining
from SampleSuperstoreComplete_Order as o

--join the order dataset with the return dataset aliasing as s
join Sample_Superstore_Complete as s

--create a join using the order ids of both datasets
on o.Order_ID = s.Order_ID

--filter returned as yes
where returned = 'yes'

--group by product name and id
group by Product_Name, Product_ID

--order by product count in descending order
order by  product_count desc;
```
![image](https://github.com/oenijesiku/Wunmi_portfolio/assets/87021092/b4d7a6ee-3b13-4aa4-9987-32f083dde52e)

**Day 26 Question**: Using the employee table dataset, write a query to show the ratio of the analyst job title to the entire job titles.
#### Query
```sql
--count the analyst job title and the total count of job title
select count(case when job_title ='Analyst' then 1 else NULL end) as AnalystCount,
		count(job_title) as AnalystToTotalCount

--from the employee dataset
from Employee_Table
```
![image](https://github.com/oenijesiku/Wunmi_portfolio/assets/87021092/00e6ca82-1a2f-472b-8fbe-94ddc525eefa)

**Day 27 Question**: Write a query to find the 3rd highest sales from the sample superstore data.
#### Query
```sql
select top 1 round(sales,2)
from(
select top 3 Sales
from Sample_Superstore_Complete
order by Sales desc
) as subquery
order by Sales asc;
```
![image](https://github.com/oenijesiku/Wunmi_portfolio/assets/87021092/a4056101-12e4-4714-b976-a9f8837e95b5)

**Day 29 Question**: Using the Employee dataset, please write a query to show the job title and department with the highest salary.
#### Query
```sql
select top 1 job_title, department
from Employee_Table
where salary = (select max(salary) from Employee_Table)
```
![image](https://github.com/oenijesiku/Wunmi_portfolio/assets/87021092/49f20986-d707-4a68-be7e-86d394cc36ce)

**Day 30 Question**: Using the Employee dataset, write a query to determine the rank of employees based on their salaries in each department. For each department, find the employee(s) with the highest salary and rank them in Desc order.
#### Query
```sql
with Rankedemployees as (
select first_name, last_name, department, salary, dense_rank() over (partition by department order by salary desc) as department_salary_rank
from Employee_Table
)

select first_name, last_name, department, salary, department_salary_rank
from Rankedemployees
```
![image](https://github.com/oenijesiku/Wunmi_portfolio/assets/87021092/6a4ebf20-92e0-4f84-993d-c9bf0a8c6aa8)
