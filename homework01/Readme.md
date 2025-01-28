# Module 1 Homework: Docker & SQL

## Question 1
```
docker run -it --entrypoint=bash python:3.12.8
# Once above command runs, run the following to get the pip version
pip --version

#I got the following output
pip 24.3.1 from /usr/local/lib/python3.12/site-packages/pip (python 3.12)
```

## Question 3
```
SELECT 
    SUM(CASE WHEN trip_distance <= 1 THEN 1 ELSE 0 END) AS up_to_1_mile,
    SUM(CASE WHEN trip_distance > 1 AND trip_distance <= 3 THEN 1 ELSE 0 END) AS 1_to_3_miles,
    SUM(CASE WHEN trip_distance > 3 AND trip_distance <= 7 THEN 1 ELSE 0 END) AS 3_to_7_miles,
    SUM(CASE WHEN trip_distance > 7 AND trip_distance <= 10 THEN 1 ELSE 0 END) AS 7_to_10_miles,
    SUM(CASE WHEN trip_distance > 10 THEN 1 ELSE 0 END) AS over_10_miles
FROM green_tripdata
WHERE lpep_pickup_datetime >= '2019-10-01 00:00:00'
  AND lpep_pickup_datetime < '2019-11-01 00:00:00';
```


## Question 4
```
SELECT DATE(lpep_pickup_datetime) AS pickup_date FROM green_tripdata GROUP BY DATE(lpep_pickup_datetime) ORDER BY MAX(trip_distance) DESC LIMIT 1;
```

## Question 5

```
SELECT 
    l."Zone",
    COUNT(*) AS total_trips
FROM green_tripdata g
JOIN taxi_zone_lookup l
    ON g."PULocationID" = l."LocationID"
GROUP BY l."Zone"
ORDER BY total_trips DESC
LIMIT 3;
```

## Question 6
```
SELECT 
    l."Zone" AS dropoff_zone
FROM green_tripdata g
JOIN taxi_zone_lookup l
    ON g."DOLocationID" = l."LocationID"
JOIN taxi_zone_lookup pickup_zone
    ON g."PULocationID" = pickup_zone."LocationID"
WHERE pickup_zone."Zone" = 'East Harlem North'
  AND g.lpep_pickup_datetime >= '2019-10-01 00:00:00'
  AND g.lpep_pickup_datetime < '2019-11-01 00:00:00'
GROUP BY l."Zone"
ORDER BY MAX(g.tip_amount) DESC
LIMIT 1;
```
