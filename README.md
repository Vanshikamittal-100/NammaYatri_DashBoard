# Namma Yatri Ride-Sharing Data Analysis

## Project Overview
This project involves analyzing ride-sharing data from the Namma Yatri app to uncover usage patterns, optimize services, and enhance customer satisfaction. The analysis is performed using SQL for data manipulation and querying, Power BI for visualization, and Excel for additional data processing.

## Data Sources
The dataset includes information on trips, trip details, locations, duration, and payment methods. The data is structured across multiple tables, each representing different aspects of the ride-sharing service.

## Table Structures

CREATE TABLE trips (
    tripid INTEGER,
    faremethod INTEGER,
    fare INTEGER,
    loc_from INTEGER,
    loc_to INTEGER,
    driverid INTEGER,
    custid INTEGER,
    distance INTEGER,
    duration INTEGER
)
CREATE TABLE trips_details4 (
    tripid INTEGER,
    loc_from INTEGER,
    searches INTEGER,
    searches_got_estimate INTEGER,
    searches_for_quotes INTEGER,
    searches_got_quotes INTEGER,
    customer_not_cancelled INTEGER,
    driver_not_cancelled INTEGER,
    otp_entered INTEGER,
    end_ride INTEGER
);

CREATE TABLE loc (
    id INT,
    assembly1 VARCHAR(200)
);

CREATE TABLE duration (
    id INT,
    duration VARCHAR(200)
);

CREATE TABLE payment (
    id INT,
    method VARCHAR(200)
);

Analysis and Queries:

## Total Trips:
SELECT COUNT(DISTINCT tripid) FROM trips_details4;

## Total Drivers:
SELECT COUNT(DISTINCT driverid) FROM trips;

## Total Earnings:
SELECT SUM(fare) FROM trips;

## Total Completed Trips:
SELECT SUM(end_ride) FROM trips_details4;

## Total Searches and Related Metrics:
SELECT SUM(searches), SUM(searches_got_estimate), SUM(searches_for_quotes), SUM(searches_got_quotes),
       SUM(customer_not_cancelled), SUM(driver_not_cancelled), SUM(otp_entered), SUM(end_ride)
FROM trips_details4;

## Average Fare per Trip:
SELECT SUM(fare) / COUNT(*) FROM trips;

## Top 5 Earning Drivers:
select * from 
(select *,dense_rank() over(order by fare desc) rnk
from
(select driverid,sum(fare)fare from trips group by driverid)b)c 
where rnk<6;


## DASHBOARD CREATION:
Using Power BI, a comprehensive dashboard was created to visualize the insights gained from the data analysis. The dashboard includes:
1.Completed trips
2.Searches 
3.Estimates
4.Quotes
5.Driver Earnings
6.Conversion Rate
7.Trips Vs.Duration
8.Fare Vs.Duration
9.Distance Vs.Duration
10.table
11.map

## Key Metrics and Findings:
Conversion Rate: Calculated as SUM(end_ride) / SUM(searches)

## Conclusion
This project provided a detailed analysis of the Namma Yatri ride-sharing data, highlighting key areas for service optimization and customer satisfaction improvement. The insights gained can help in strategic decision-making for better resource allocation and service enhancements.

## Report Snapshot (Power BI DESKTOP)
![image](https://github.com/user-attachments/assets/c328302c-3909-4f65-8710-27b2f7fcc2cb)
