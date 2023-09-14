
# Data Dig

We’ve curated a set of interesting data sets for you: NASA astronauts, Superbowl results, Pokemon stats, NBA players, Top movies, Top countries by population, Solar system objects by size, Marvel characters, Furniture store sales, Earned KA badges, Winston's donut logs, Card game results, and NFL draft picks.

Pick one of those data sets or create a data set like that, and use advanced SELECT queries to discover things about the data. What sort of questions might one have about that data, like if they were using it for an app or a business idea? Here are some ideas:

What are average, max, and min values in the data?  
What about those numbers per category in the data (using HAVING)?    
What ways are there to group the data values that don’t exist yet (using CASE)?   
What interesting ways are there to filter the data (using AND/OR)?   

```sql
select count(*), 
product
from sales
group by product;
```

| count(*) | product | 
| :--: | :---: |
| 4 |	Bed |
| 84 | Chair |
| 12 | Couch |


select avg(price) from sales;   
select max(price) from sales;    
select min(price) from sales;   

avg(price)      
1740   

max(price)   
7500   

min(price)   
1200   

```sql
select COUNT (payment_type),    
payment_type 
from sales  
group by payment_type;
```
| COUNT (PAYMENT TYPE) | PAYMENT TYPE |
| :--: | :---: |
| 7 |	Amex |
| 11 | Diners |
| 33 | Mastercard |
| 49 | Visa |

```sql
select product, min(price) from sales;
select product, max(price) from sales;
```

```sql
select product,
price,
transaction_date
from sales
group by product;
```
RESULTS

| product |	min(price) |
| :--: | :---: |
| Chair |	1200 |

| product |	max(price)|
| :--: | :---: |
| Bed |	7500 |

| product | price |	transaction_date |
| :--: | :---: | :---: |
| Bed |	7500 | 1/8/09 15:16 |
| Chair |	1200 |	1/13/09 19:39 |
| Couch |	3600 |	1/5/09 8:58 |

```sql
select product, 
price, 
city
from sales
where country = "United states" and price > 1500 
group by city;
```
RESULTS

| product |	price	| city |   
| :--: | :---: | :--: |   
| Couch |	3600 | Cahaba Heights |   
| Couch |	3600 | Delray Beach |   
| Couch |	3600 | Flossmoor |   
| Couch |	3600 |	Irvine |   
| Bed |	7500 | Miami |   
| Bed |	7500 | New Rochelle |   
| Couch |	3600 | Pittsfield |   
| Couch |	3600 | Sandy Springs |   
| Bed |	7500 | Woodsboro |   

```sql
select product, 
price, 
city
from sales
where state = "FL" OR state = "NY";
```   
RESULTS 

| product |	price | city |   
| :--: | :---: | :--: |    
| Chair |	1200 | New York |
| Chair |	1200 | New York |
| Chair |	1200 | New York |  
| Bed	| 7500 | Miami |   
| Chair |	1200 | Brooklyn |   
| Couch |	3600 | Delray Beach |   
| Chair |	1200 | Fort Lauderdale |   
| Bed |	7500 | New Rochelle |   
| Chair |	1200 | Staten Island |     
| Chair |	1200 | Amelia Island |  
| Chair |	1200 | Coral Gables |   
| Chair |	1200 | Miami |   

```sql   
select count(*),   
case   
when price >= 7000 then "Luxury items"   
when price = 3600 then "standard items"  
ELSE "discount items"   
end items   
from sales   
group by items;  
```
 RESULTS
 
| count(*) | items |   
| :--: | :---: |   
| 4 |	Luxury items |    
| 84 | discount items |   
| 12 | standard items |  


```sql   
select product,   
AVG(price) as avg_price   
from sales   
group by product   
having avg_price > 1500;   
```   

RESULTS

| product	| avg_price |
| :--: | :---: | 
| Bed |	7500 |
| Couch |	3600 |
