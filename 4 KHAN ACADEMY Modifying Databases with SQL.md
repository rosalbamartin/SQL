# Modifying data bases with SQL  

## Project: App impersonator  

Google Classroom
Think about your favorite apps, and pick one that stores your data- like a game that stores scores, an app that lets you post updates, etc. Now in this project, you're going to imagine that the app stores your data in a SQL database (which is pretty likely!), and write SQL statements that might look like their own SQL.

CREATE a table to store the data.   
INSERT a few example rows in the table.    
Use an UPDATE to emulate what happens when you edit data in the app.    
Use a DELETE to emulate what happens when you delete data in the app.    
   
    
CREATE TABLE meal_planning (   
    id INTEGER PRIMARY KEY,   
    Day TEXT,   
    Breakfast TEXT,   
    Lunch TEXT,    
    Snack TEXT,   
    Dinner TEXT,   
    total_calories INTEGER   
    );   


INSERT INTO meal_planning (Day, Breakfast, Lunch, Snack, Dinner, Total_calories) VALUES ("Monday", "cheese Omelete", "chicken with spinach quiche", "apple", "vegetables soup", 1100);   
INSERT INTO meal_planning (Day, Breakfast, Lunch, Snack, Dinner, Total_calories) VALUES ("Tuesday", "Yogurt with fruits", "Tuna salad", "orange", "veggie burrito", 1350);    
INSERT INTO meal_planning (Day, Breakfast, Lunch, Snack, Dinner, Total_calories) VALUES ("Wednesday", "granola bar", "grilled fish with tomato salad", "Strawberry jelly", "Hummus with carrots and celery", 1050);   
INSERT INTO meal_planning (Day, Breakfast, Lunch, Snack, Dinner, Total_calories) VALUES ("Thursday", "Protein Shake", "Primavera pasta", "Blue berries & yogurt", "Tomato Soup", 1300);   
INSERT INTO meal_planning (Day, Breakfast, Lunch, Snack, Dinner, Total_calories) VALUES ("Friday", "Ezequiel bread sandwich", "Quinoa veggie Poke Bowl", "Orange", "Cauliflower crust pizza", 1400);   
INSERT INTO meal_planning (Day, Breakfast, Lunch, Snack, Dinner, Total_calories) VALUES ("Saturday", "avocado toast", "sushi", "protein bar", "Lentils & vegetables soup", 1250);   
INSERT INTO meal_planning (Day, Breakfast, Lunch, Snack, Dinner, Total_calories) VALUES ("Sunday", "Hard boiled eggs", "garbanzo beans salad", "Strawberries & cream", "cucumber salad", 1500);   
INSERT INTO meal_planning (Day, Breakfast, Lunch, Snack, Dinner, Total_calories) VALUES ("Monday of fasting", "fasting day", "no food", "no food", "no food", 0);   
   
```sql
select *
from meal_planning;
```
QUERY RESULTS

| id | Day | Breakfast | Lunch | Snack | Dinner |	Total_calories |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| 1 |	Monday | cheese Omelete |	chicken with spinach quiche |	apple |	vegetables soup |	1100 |
| 2 |	Tuesday |	Yogurt with fruits | Tuna salad	| orange | veggie burrito |	1350 |
| 3 |	Wednesday	| granola bar |	grilled fish with tomato salad | Strawberry jelly |	Hummus with carrots and celery | 1050 |
| 4	| Thursday | Protein Shake | Primavera pasta | Blue berries & yogurt | Tomato Soup | 1300 |
| 5	| Friday | Ezequiel bread sandwich | Quinoa veggie Poke Bowl |Orange	| Cauliflower crust pizza |	1400 |
| 6	| Saturday | avocado toast | sushi | protein bar | Lentils & vegetables soup | 1250 |
| 7 |	Sunday | Hard boiled eggs |	garbanzo beans salad | Strawberries & cream |	cucumber salad | 1500 |
| 8 |	Monday | fasting day | no food | no food |no food |	no food	|

```sql
UPDATE meal_planning SET snack = "orange or any fruit" WHERE id = 5;
```

```sql
DELETE FROM meal_planning WHERE id = 8;
select * from meal_planning;
```
