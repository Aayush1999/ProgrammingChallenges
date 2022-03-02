# SQL Challenge

The database contains two tables, store_revenue and marketing_data.  Refer to the two CSV
files, store_revenue and marketing_data to understand how these tables have been created.

store_revenue contains revenue by date, brand ID, and location:

 >  create table store_revenue (
 >     id int not null primary key auto_increment,
 >    date datetime,
 >    brand_id int,
 >    store_location varchar(250),
 >    revenue float  
 >  );

marketing_data contains ad impression and click data by date and location:

> create table marketing_data (
>  id int not null primary key auto_increment,
>  date datetime,
>  geo varchar(2),
>  impressions float,
>  clicks float
> );

### Please provide a SQL statement under each question.

* Question #0 (Already done for you as an example)
 Select the first 2 rows from the marketing data
​
>  select *
>  from marketing_data
> limit 2;
​
*  Question #1
 Generate a query to get the sum of the clicks of the marketing data
>  select sum(clicks) as SumOfClicks
>  from marketing_data;
​
*  Question #2
 Generate a query to gather the sum of revenue by geo from the store_revenue table
>  select store_location, sum(revenue) as Revenue
>  from store_revenue
>  group by store_location
​
*  Question #3
 Merge these two datasets so we can see impressions, clicks, and revenue together by date
and geo.
 Please ensure all records from each table are accounted for.
>  select sr.date, md.geo, sr.store_location, impressions, clicks, revenue 
>  from marketing_data md left join store_revenue sr on sr.date = md.date
>  group by sr.date, md.geo
​
* Question #4
 In your opinion, what is the most efficient store and why?
> select md.geo, sum(clicks) + sum(impressions) as Total
> from marketing_data md
> group by md.geo
> order by Total DESC
- From the above query, we find that MN has the greatest amount of social media response at 23293, CA has the second highest at 22879, NY has the third-highest at 20270 and TX has the lowest at 17081.
> select sr.store_location, sum(revenue) as Revenue
> from store_revenue sr
> group by store_location
> order by Revenue desc limit 10
- From the revenue query above we find that CA has the highest revenue of all stores. However, when we look at the data carefully, this value is heavily inflated by a 234234 value on the 3rd of January which is most likely a typo and does not fit the trend of revenues. Also, there is a 45235 revenue value for NY on the 4th of January that does not seem to align with the revenue trends of the state, suggesting another typo. Removing these values, we get that TX has the highest revenue value at $9629, NY has the second highest revenue at $6749 and CA has the third highest revenue at $1003. To calculate the most efficient store based on the above 2 queries, I will be using a (revenue/(clicks + impressions)) formula. Based on this formula, the store in TX makes $0.56 per click and impression, NY makes $0.33 per click and impression, while CA makes $0.044 per click and impression. Therefore, in my opinion, TX is the most efficient store as it generates more income per click and impression.

​
* Question #5 (Challenge)
 Generate a query to rank in order the top 10 revenue producing states
> select sr.store_location, sum(revenue) as Revenue
> from store_revenue sr
> group by store_location
> order by Revenue desc limit 10
​
