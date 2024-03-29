# Health Analytics Mini Case Study
## DEBUG SQL SCRIPT
### 1. How many unique users exist in the logs dataset?
````sql
SELECT
  COUNT DISTINCT user_id
FROM health.user_logs;
````
**ANSWER:**
unique _users:
554

### for questions 2-8 we created a temporary table
````sql
DROP TABLE IF EXISTS user_measure_count;
CREATE TEMP TABLE user_measure_cout
SELECT
    id,
    COUNT(*) AS measure_count,
    COUNT(DISTINCT measure) as unique_measures
  FROM health.user_logs
  GROUP BY 1; 
````

### 2. How many total measurements do we have per user on average?
````sql
SELECT
  ROUND(MEAN(measure_count))
FROM user_measure_count;
````
**ANSWER:**
avg_measurement
79.23

### 3. What about the median number of measurements per user?
````sql
SELECT
  PERCENTILE_CONTINUOUS(0.5) WITHIN GROUP (ORDER BY id) AS median_value
FROM user_measure_count;
````
**ANSWER:**
median_value
2

### 4. How many users have 3 or more measurements?
````sql
SELECT
  COUNT(*)
FROM user_measure_count
HAVING measure >= 3;
````
**ANSWER:**
count
209

### 5. How many users have 1,000 or more measurements?
````sql
SELECT
  SUM(id)
FROM user_measure_count
WHERE measure_count >= 1000;
````
**ANSWER:**
count
5

### 6. Have logged blood glucose measurements?
````sql
SELECT
  COUNT DISTINCT id
FROM health.user_logs
WHERE measure is 'blood_sugar';
````
**ANSWER:**
#### measure  blood glucose      
#### unique_blood_glucose_user  325     
#### percentage 40.22

### 7. Have at least 2 types of measurements?
````sql
SELECT
  COUNT(*)
FROM user_measure_count
WHERE COUNT(DISTINCT measures) >= 2;
````
**ANSWER:**

#### unique_user   204
#### unique_user_percentage   36.82


### 8. Have all 3 measures - blood glucose, weight and blood pressure?
````sql
WITH all_measures AS (
SELECT *
FROM user_measure_count
WHERE unique_measure_count = 3)

SELECT
  COUNT(DISTINCT m.id) AS unique_user,
  ROUND(COUNT(DISTINCT m.id)::numeric / COUNT(DISTINCT u.id),2) AS unique_user_percentage
FROM user_measure_count AS u
LEFT JOIN all_measures AS m
  ON u.id = m.id;
````

**ANSWER:**
#### unique_user  50      
#### unique_user_percentage  9.03


### 9.  What is the median systolic/diastolic blood pressure values?
````sql
SELECT
  'blood_pressure' AS measure_name,
  PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY systolic) AS systolic_median,
  PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY diastolic) AS diastolic_median
FROM health.user_logs
WHERE measure = 'blood_pressure';
````
**ANSWER:**
#### measure_name     blood_presure
#### systolic_median  126   
#### diastolic_median 79
