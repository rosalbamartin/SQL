# Relational Queries in SQL

# Project: Famous people


In this project, you’re going to make your own table with some small set of “famous people”, then make more tables about things they do and join those to create nice human readable lists.
For example, here are types of famous people and the questions your data could answer:  
•	Movie stars: What movies are they in? Are they married to each other?  
•	Singers: What songs did they write? Where are they from?  
•	Authors: What books did they write?   
•	Fictional characters: How are they related to other characters? What books do they show up in?       
    
CREATE TABLE Famous_People (   
    id INTEGER PRIMARY KEY AUTOINCREMENT,   
    Artist TEXT,   
    Age INTEGER, 
    Nationality TEXT,  
    Occupation TEXT);      
    
INSERT INTO Famous_People (Artist, Age, Nationality, Occupation) VALUES ("Madonna",65,"American","singer");    
INSERT INTO Famous_People (Artist, Age, Nationality, Occupation) VALUES ("Tom Cruise", 61,"American","actor");  
INSERT INTO Famous_People (Artist, Age, Nationality, Occupation) VALUES ("Ed Sheeran", 32,"British","singer");  
INSERT INTO Famous_People (Artist, Age, Nationality, Occupation) VALUES ("Adele", 35,"British","singer");  
INSERT INTO  Famous_People (Artist, Age, Nationality, Occupation) VALUES ("Bruno Mars", 37,"American","singer");  
INSERT INTO  Famous_People (Artist, Age, Nationality, Occupation) VALUES ("Cameron Diaz", 51,"American", "actress");       
INSERT INTO  Famous_People (Artist, Age, Nationality, Occupation) VALUES ("Leonardo DiCaprio", 48,"American", "actor");   
INSERT INTO Famous_People (Artist, Age, Nationality, Occupation) VALUES ("Shakira",44,"Colombian","singer");  
INSERT INTO Famous_People (Artist, Age, Nationality, Occupation) VALUES ("Gloria Stefan",66,"Cuban-American","singer");  
INSERT INTO  Famous_People (Artist, Age, Nationality, Occupation) VALUES ("Will Smith", 55,"American", "actor");    
  
  
CREATE TABLE Songs_Movies (  
    id INTEGER PRIMARY KEY AUTOINCREMENT,  
    Artist TEXT,   
    greatest_hit_movie TEXT,  
    year_released INTEGER);                           
         
INSERT INTO Songs_Movies (Artist, greatest_hit_movie, year_released) VALUES ("Madonna","Like a Virgin", 1984);       
INSERT INTO Songs_Movies (Artist, greatest_hit_movie, year_released) VALUES ("Tom Cruise","Top Gun", 1986);       
INSERT INTO Songs_Movies (Artist, greatest_hit_movie, year_released) VALUES ("Adele","Rolling in the Deep" ,2011);     
INSERT INTO Songs_Movies (Artist, greatest_hit_movie, year_released) VALUES ("Will Smith","The Fresh Prince of Bel-Air", 1990);         
INSERT INTO Songs_Movies (Artist, greatest_hit_movie, year_released) VALUES ("Ed Sheeran","Shape of You", 2017);       
INSERT INTO Songs_Movies (Artist, greatest_hit_movie, year_released) VALUES ("Bruno Mars","uptown Funk", 2015);      
INSERT INTO Songs_Movies (Artist, greatest_hit_movie, year_released) VALUES ("Cameron Diaz","There's something about Mary", 1998);     
INSERT INTO Songs_Movies (Artist, greatest_hit_movie, year_released) VALUES ("Gloria Stefan","Anything for You", 1997);     
INSERT INTO Songs_Movies (Artist, greatest_hit_movie, year_released) VALUES ("Shakira", "Hips don't lie", 2022);              
INSERT INTO Songs_Movies (Artist, greatest_hit_movie, year_released) VALUES ("Leonardo DiCaprio", "Titanic", 1997);       

```sql    
select *  
from Songs_Movies;
```
```sql  
select *  
from famous_people;
```

```sql
Select 
Famous_People.Artist,  
Famous_People.Nationality,   
Famous_People.Occupation,  
Songs_Movies.greatest_hit_movie,   
Songs_Movies.year_released           
from Famous_People    
join Songs_Movies   
on Famous_People.Artist = Songs_Movies.Artist;
```

### QUERY RESULTS

| Artist | Nationality | Occupation |	Greatest_hit_movie | Year_released |
| :---: | :---: | :---: | :---: | :---: |
| Madonna |	American | singer |	Like a Virgin |	1984 |
| Tom Cruise | American |	actor |	Top Gun |	1986 |
| Ed Sheeran | British | singer |	Shape of You | 2017 |
| Adele |	British |	singer | Rolling in the Deep|	2011 |
| Bruno Mars | American |	singer | uptown Funk | 2015 |
| Cameron Diaz | American |	actress |	There's something about Mary | 1998 |
| Leonardo DiCaprio  | American | actor |	Titanic |	1997 |
| Shakira |	Colombian |	singer | Hips don't lie |	2022 |
| Gloria Stefan |	Cuban-American | singer |	Anything for You | 1997 |
| Will Smith | American |	actor |The Fresh Prince of Bel-Air | 1990 |

```sql
Select
Famous_People.Artist,
Famous_People.Nationality,
Famous_People.Occupation,
Songs_Movies.greatest_hit_movie, 
Songs_Movies.year_released
from Famous_People
join Songs_Movies
on Famous_People.Artist = Songs_Movies.Artist
where Nationality = "American" AND year_released < 2000;
```

### QUERY RESULTS

| Artist | Nationality | Occupation |	Greatest_hit_movie | Year_released |
| :---: | :---: | :---: | :---: | :---: |
| Madonna	| American | singer	| Like a Virgin |	1984 |
| Tom Cruise| American | actor | Top Gun | 1986 |
| Cameron Diaz | American |	actress |	There's something about Mary | 1998 |
| Leonardo DiCaprio |	American | actor | Titanic | 1997 |
| Will Smith | American |	actor |	The Fresh Prince of Bel-Air |	1990 |




