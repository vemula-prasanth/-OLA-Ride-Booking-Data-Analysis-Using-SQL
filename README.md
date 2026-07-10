### OLA-Ride-Booking-Data-Analysis-Using-SQL

![netflix logo](https://github.com/vemula-prasanth/-OLA-Ride-Booking-Data-Analysis-Using-SQL/blob/main/OLA%20LOGO.jpeg)


### Overview

This project analyzes OLA ride booking data using SQL. The main goal is to explore the dataset and find useful business insights by writing SQL queries.

### Objective
Analyze ride bookings.
Find successful and cancelled rides.
Analyze customer and driver ratings.
Find total revenue and booking trends.
Analyze payment methods and vehicle types.
Solve business problems using SQL.

### Dataset

The dataset contains OLA ride booking information such as booking status, customer details, vehicle type, payment method, ride distance, ratings, booking value, and cancellation reasons.

[Dataset Source](https://www.kaggle.com/datasets/muhammadahmadmujahid/ola-dataset)


### Schema
```sql
DROP TABLE IF EXISTS bengaluru_ola_rides;
```

```sql
CREATE TABLE bengaluru_ola_rides (
    Date VARCHAR(50),
    Time VARCHAR(50),
    Booking_ID VARCHAR(50) PRIMARY KEY,
    Booking_Status VARCHAR(50),
    Customer_ID VARCHAR(50),
    Vehicle_Type VARCHAR(50),
    Pickup_Location VARCHAR(100),
    Drop_Location VARCHAR(100),
    V_TAT VARCHAR(50),
    C_TAT VARCHAR(50),
    Canceled_Rides_by_Customer VARCHAR(50),
    Canceled_Rides_by_Driver VARCHAR(50),
    Incomplete_Rides VARCHAR(50),
    Incomplete_Rides_Reason TEXT,
    Booking_Value VARCHAR(50),
    Payment_Method VARCHAR(50),
    Ride_Distance VARCHAR(50),
    Driver_Ratings VARCHAR(50),
    Customer_Rating VARCHAR(50),
    Vehicle_Images TEXT
);
```

```sql
select * from bengaluru_ola_rides;
```
### 18 business problems and solutions

 ## Question 1: Retrieve all successful bookings.
```sql
SELECT * 
FROM bengaluru_ola_rides 
WHERE Booking_Status = 'Success';
```

## Question 2: Calculate the total booking value of successful rides.
```sql
SELECT SUM(Booking_Value::NUMERIC) AS Total_Revenue
FROM bengaluru_ola_rides
WHERE Booking_Status = 'Success';
```

## Question 3: Get the total number of rides cancelled by customerS.
```sql
SELECT COUNT(*) AS Total_Cancelled_by_Customers
FROM bengaluru_ola_rides
WHERE Booking_Status = 'Canceled by Customer';
```

## Question 4: List the Top 5 customers who booked the highest number of rides.

```sql
SELECT Customer_ID, 
       COUNT(*) AS Total_Rides
FROM bengaluru_ola_rides
GROUP BY Customer_ID
ORDER BY Total_Rides DESC
LIMIT 5;
```

## Question 5: Find the number of rides cancelled by drivers due to personal & car-related issues.
```sql
SELECT COUNT(*) AS Driver_Cancellations
FROM bengaluru_ola_rides
WHERE Canceled_Rides_by_Driver = 'Personal & Car related issue';
```

## Question 6: Retrieve all rides where the payment method is UPI.
```sql
SELECT * 
FROM bengaluru_ola_rides 
WHERE Payment_Method = 'UPI';
```

## Question 7: List all incomplete rides along with their reasons.
```sql
SELECT Booking_ID, Vehicle_Type, Incomplete_Rides_Reason
FROM bengaluru_ola_rides
WHERE Incomplete_Rides_Reason != NULL AND Incomplete_Rides_Reason != 'NA';
```

## Question 8: Find the vehicle type that generated the highest total revenue.

```sql
SELECT Vehicle_Type, 
       SUM(Booking_Value::NUMERIC) AS Total_Revenue
FROM bengaluru_ola_rides
WHERE Booking_Status = 'Success'
GROUP BY Vehicle_Type
ORDER BY Total_Revenue DESC
LIMIT 1;
```

## Question 9: List the Top 10 customers based on total booking value.
```sql

SELECT Customer_ID, 
       SUM(Booking_Value::NUMERIC) AS Total_Spend
FROM bengaluru_ola_rides
WHERE Booking_Status = 'Success'
GROUP BY Customer_ID
ORDER BY Total_Spend DESC
LIMIT 10;
```

## Question 10: Find the most preferred payment method.

```sql
SELECT Payment_Method, 
       COUNT(*) AS Usage_Count
FROM bengaluru_ola_rides
WHERE Payment_Method != 'null'
GROUP BY Payment_Method
ORDER BY Usage_Count DESC
LIMIT 1;
```

## Question 11: Find the average booking value for each vehicle type.
```sql
SELECT Vehicle_Type, 
       ROUND(AVG(Booking_Value::NUMERIC), 2) AS Avg_Amount
FROM bengaluru_ola_rides
WHERE Booking_Status = 'Success'
GROUP BY Vehicle_Type;
```

## Question 12: Find the pickup locations with the highest number of bookings.
```sql
SELECT Pickup_Location, 
       COUNT(*) AS Bookings
FROM bengaluru_ola_rides
GROUP BY Pickup_Location
ORDER BY Bookings DESC
LIMIT 5;

```
## Question 13: Find the drop locations with the highest number of completed rides.
```sql
SELECT Drop_Location, 
       COUNT(*) AS Completed_Rides
FROM bengaluru_ola_rides
WHERE Booking_Status = 'Success'
GROUP BY Drop_Location
ORDER BY Completed_Rides DESC
LIMIT 5;
```

## Question 14: Count successful bookings for each vehicle type.
```sql
SELECT Vehicle_Type, 
       COUNT(*) AS Success_Count
FROM bengaluru_ola_rides
WHERE Booking_Status = 'Success'
GROUP BY Vehicle_Type;
```

## Question 15: Count cancelled bookings for each vehicle type.
```sql
SELECT Vehicle_Type, 
       COUNT(*) AS Cancel_Count
FROM bengaluru_ola_rides
WHERE Booking_Status LIKE 'Canceled%'
GROUP BY Vehicle_Type;
```

## Question 16: List the Top 5 days with the highest booking revenue.
```sql

SELECT Date, 
       SUM(Booking_Value::NUMERIC) AS Daily_Revenue
FROM bengaluru_ola_rides
WHERE Booking_Status = 'Success'
GROUP BY Date
ORDER BY Daily_Revenue DESC
LIMIT 5;
```

## Question 17: Find the payment method that generated the highest revenue.
```sql

SELECT Payment_Method, 
       SUM(Booking_Value::NUMERIC) AS Total_Revenue
FROM bengaluru_ola_rides
WHERE Booking_Status = 'Success'
GROUP BY Payment_Method
ORDER BY Total_Revenue DESC
LIMIT 1;
```

## Question 18: Find the booking status-wise count of rides.
```sql

SELECT Booking_Status, 
       COUNT(*) AS Total_Rides
FROM bengaluru_ola_rides
GROUP BY Booking_Status
ORDER BY Total_Rides DESC;
```

### created by vemula prasanth

### connect with me:[linkedin](https://www.linkedin.com/in/prasanth-vemula-74702b2b6?utm_source=share_via&utm_content=profile&utm_medium=member_android)



















