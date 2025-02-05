# Module 1 Homework: Docker & SQL

## Question 1: Within the execution for Yellow Taxi data for the year 2020 and month 12: what is the uncompressed file size (i.e. the output file yellow_tripdata_2020-12.csv of the extract task)?
#### Answer: 128.3 MB


## Question 2: What is the rendered value of the variable file when the inputs taxi is set to green, year is set to 2020, and month is set to 04 during execution?
#### Answer: {{inputs.taxi}}__tripdata_{{inputs.year}}-{{inputs.month}}.csv


## Question 3: How many rows are there for the Yellow Taxi data for all CSV files in the year 2020?
#### Answer: 24,648,499
#### Multiple ways to do this
For GCP: dezoomcamp2025-449806 is my project id
```
SELECT count(*)  
FROM `dezoomcamp2025-449806.yellow_tripdata` 
WHERE  filename like 'yellow_tripdata_2020%'

SELECT count(*)  
FROM `dezoomcamp2025-449806.yellow_tripdata` 
WHERE  filename like '%2020%'
```

For Postgres
```
SELECT count(*)  
FROM yellow_tripdata
WHERE  filename like 'yellow_tripdata_2020%'

SELECT count(*)  
FROM yellow_tripdata
WHERE filename like '%2020%'
```

## Question 4: How many rows are there for the Green Taxi data for all CSV files in the year 2020?
#### Answer: 1,734,051 
Similar to question 3. Query is below for postgres
```
SELECT count(*)  
FROM green_tripdata
WHERE  filename like 'green_tripdata_2020%'

SELECT count(*)  
FROM green_tripdata
WHERE filename like '%2020%'
```

## Question 5: How many rows are there for the Yellow Taxi data for the March 2021 CSV file?
#### Answer: 1925152
```
SELECT COUNT(*) FROM `dezoomcamp2025-449806.yellow_tripdata` WHERE filename='yellow_tripdata_2021-03.csv'
```

## Question 6: How would you configure the timezone to New York in a Schedule trigger?
#### Answer: Add America/New_York timezone property in the schedule trigger configuration.
```
triggers:
  - id: daily
    type: io.kestra.plugin.core.trigger.Schedule
    cron: "@daily"
    timezone: America/New_York
```
