# UK-Train-Rides-Tickets-Data-SQL-project

## Objectives

This is my first project on my journey to becoming a data analyst, In this project, I analyzed UK train ticket sales data to gain insights into revenue, customer preferences, and common causes of delays. This analysis helps understand how and where revenue is generated, which stations and routes are popular, and the key factors that impact customer experiences, such as delays.

## Dataset
The data for this project is sourced from the Maven analytics dataset. <br>
**Dataset Link** (https://mavenanalytics.io/data-playground?pageSize=10) <br>
Mock train ticket data for National Rail in the UK, from Jan to Apr 2024, including details on the type of ticket, the date & time for each journey, the departure & arrival stations, the ticket price, and more.



Creating new database called Railway
```sql
create database railway
```

Creating Table called Tickets

```sql
create table Tickets (
Transaction_ID	varchar (20),
Date_of_Purchase date,	
Time_of_Purchase	time,
Purchase_Type	varchar (20),
Payment_Method	varchar (20),
Railcard	varchar (20),
Ticket_Class	varchar (20),
Ticket_Type	varchar (20),
Price	float,
Departure_Station	varchar (30),
Arrival_Destination	varchar (30),
Date_of_Journey_date date,
Departure_Time	time,
Arrival_Time	time,
Actual_Arrival_Time	 time,
Journey_Status	varchar (30),
Reason_for_Delay	varchar (30),
Refund_Request varchar (30),
)
```

View everthing in our table
```sql
select * from tickets
```

Here are 10 potential problem questions to explore and analyze with this railway data.
These questions will cover revenue, customer preferences, and delay reasons, providing a variety of angles for analysis.


1.What is the total revenue generated from ticket sales?
```sql
select 
	sum (price) as Total_revenue
from tickets
```

2.What is the average ticket price for each class (e.g., Standard, First Class)?
```sql
select
	ticket_class, 
	avg (price) as Avg_price
from tickets
group by ticket_class
```
3.Which departure station had the highest number of ticket purchases?
```sql
select top 1
	Departure_Station,
	sum (price) as Ticket_Count
from tickets
group by Departure_Station
order by Departure_Station desc
```

4.What are the most common reasons for train delays?
```sql
select top 1
	Reason_for_Delay,
	count(reason_for_delay) as Delay_count
from tickets
where Reason_for_Delay is not null
group by Reason_for_delay
order by Delay_count desc
```

5.How many tickets were purchased online compared to those purchased at the station?
```sql
select 
	Purchase_Type,
	count (purchase_type) as Purchase_count
from tickets
group by Purchase_Type	
```
6.How many tickets were purchased with each payment method?
```sql
select 
	Payment_Method,
	sum(price) as Ticket_count
from tickets
group by Payment_Method
```

7.What is the total number of journeys for each month?
```sql
Select format(cast(Date_of_Journey as date), 'yyyy-MM') as month, 
       COUNT(*) AS Journey_Count
from tickets
group by format(cast(Date_of_Journey as date), 'yyyy-MM');
```


8.How many tickets were sold per ticket type (e.g., Advance, Anytime)?

```sql
select 
	Ticket_Type,
	count (*) as Ticket_count
from tickets
group by Ticket_Type
```


9.How many journeys experienced delays specifically due to signal failures?

```sql
SELECT COUNT(*) AS Signal_Failure_Delays
FROM tickets
WHERE Journey_Status = 'Delayed' AND Reason_for_Delay = 'Signal Failure';
```


10.Which railcard type is associated with the highest average ticket price?
```sql
select top 1 Railcard, AVG(Price) AS Average_Price
FROM tickets
GROUP BY Railcard
ORDER BY Average_Price DESC
```


## Author – Qasim Ali Mahamed
This project is part of my portfolio, showcasing the SQL skills essential for data analyst roles. If you have any questions, feedback, or would like to collaborate, feel free to get in touch!

## End Project
