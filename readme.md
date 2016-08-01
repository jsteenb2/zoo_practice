
## BASIC

1.

```sql
SELECT population FROM world
  WHERE name = 'Germany';
```

2.

```sql
  SELECT name, population FROM world
  WHERE name IN ('Ireland', 'Iceland', 'Denmark');
```

3.

```sql
  SELECT name, area FROM world
  WHERE area BETWEEN 200000 AND 250000;
```

## SELECT from WORLD

1.

```sql
SELECT name, continent, population FROM world
```

2.

```sql
SELECT name FROM world
WHERE population>200000000
```
3.

```sql
SELECT name, gdp/population FROM world
WHERE population>200000000
```

4.

```sql
SELECT name, population/1000000 FROM world
WHERE continent = 'South America'
```

5.

```sql
SELECT name, population FROM world
WHERE name IN ('France', 'Germany', 'Italy')
```

6.

```sql
SELECT name FROM world
WHERE name LIKE '%UNITED%'
```

7.

```sql
SELECT name, population, area FROM world
WHERE area > 3000000
OR population > 250000000
```

8.

```sql
SELECT name, population, area FROM world
WHERE area > 3000000
XOR population > 250000000
```

9.

```sql
SELECT name, ROUND(population/1000000,2), ROUND(gdp/1000000000,2) FROM world
WHERE continent = 'South America'
```
10.

```sql
SELECT name, ROUND(gdp/population,-3) FROM world
WHERE gdp > 1000000000000
```
11.

```sql
SELECT name,
       CASE WHEN continent='Oceania' THEN 'Australasia'
            ELSE continent END
  FROM world
 WHERE name LIKE 'N%'
 ```
 
12.

```sql
SELECT name,
  CASE WHEN continent = 'Europe' THEN 'Eurasia'
  WHEN continent = 'Asia' THEN 'Eurasia'
  WHEN continent = 'North America' THEN 'America'
  WHEN continent = 'South America' THEN 'America'
  WHEN continent = 'Caribbean' THEN 'America'
  ELSE continent END
  FROM world
 WHERE name LIKE 'A%' OR name LIKE 'B%'
```

13.

```sql
 SELECT name, continent,
  CASE WHEN continent = 'Oceania' THEN 'Australasia'
           WHEN continent = 'Eurasia' THEN 'Europe/Asia'
              WHEN name = 'Turkey' THEN 'Europe/Asia'
             WHEN name LIKE 'B%' AND continent = 'Caribbean'  THEN 'North America'  
            WHEN name NOT LIKE 'B%' AND continent = 'Caribbean' THEN 'South America'
             ELSE continent
   END
FROM world
ORDER BY name ASC
```

###Nobel

1.

```sql
SELECT yr, subject, winner
  FROM nobel
 WHERE yr = 1950
```

2.

```sql
SELECT winner
  FROM nobel
 WHERE yr = 1962
   AND subject = 'Literature'
```


3.

```sql
SELECT yr, subject FROM nobel
WHERE winner = 'Albert Einstein'
```

4.

```sql
SELECT winner FROM nobel
WHERE subject = 'Peace'
             AND  yr >= 2000
```

5.

```sql
SELECT yr, subject, winner FROM nobel
WHERE yr BETWEEN 1980 AND 1989 AND subject = 'Literature'
```

6.

```sql
SELECT * FROM nobel
 WHERE winner IN ('Theodore Roosevelt', 'Woodrow Wilson', 'Jimmy Carter')
```

7.

```sql
SELECT winner FROM nobel
WHERE winner LIKE 'John %'
```

8.

```sql
SELECT * FROM nobel
WHERE subject = 'Physics' AND yr = 1980
           OR yr = 1984 AND subject = 'Chemistry'
```

9.

```sql
SELECT * FROM nobel
WHERE subject NOT IN ('Chemistry', 'Medicine') AND yr = 1980
```

10.

```sql
SELECT * FROM nobel
WHERE subject = 'Medicine' AND yr<1910
OR subject = 'Literature' AND yr>=2004
```

11.

```sql
SELECT * FROM nobel
where winner = 'PETER GRÜNBERG'
```

12.

```sql
SELECT * FROM nobel
where winner = "EUGENE O'NEILL"
```

13.

```sql
SELECT winner, yr, subject FROM nobel
where winner LIKE 'Sir %'
ORDER BY yr DESC, winner
```

14.

```sql
SELECT winner, subject
  FROM nobel
 WHERE yr=1984
 ORDER BY subject IN ('Physics','Chemistry'),subject,winner
```

###JOIN OPERATION

1.

```sql
SELECT matchid, player FROM goal
  WHERE teamid = 'GER'
```

2.

```sql
SELECT id,stadium,team1,team2
  FROM game
WHERE id = '1012'
```

3.

```sql
SELECT player,teamid,stadium, mdate
  FROM game JOIN goal ON (id=matchid)
WHERE goal.teamid = 'GER'
```

4.

```sql
SELECT team1,team2,player
  FROM game JOIN goal ON (id=matchid)
WHERE player LIKE 'Mario%'
```

5.

```sql
SELECT player, teamid, coach, gtime
  FROM goal JOIN eteam ON teamid=id
 WHERE gtime<=10
```

6.

```sql
SELECT mdate, teamname
  FROM game JOIN eteam ON team1=eteam.id
 WHERE coach = 'Fernando Santos'
```

7.

```sql
SELECT player
 FROM game JOIN goal ON id=matchid
 WHERE stadium = 'National Stadium, Warsaw'
```

8.

```sql
SELECT DISTINCT player
  FROM game JOIN goal ON matchid = id
    WHERE (team1='GER' OR team2='GER')
AND goal.teamid != 'GER'
```

9.

```sql
SELECT eteam.teamname, COUNT(*)
  FROM goal JOIN eteam ON goal.teamid = eteam.id
  Group by eteam.teamname
```

10.

```sql
SELECT game.stadium, COUNT(*)
  FROM goal JOIN game ON goal.matchid = game.id
  Group by game.stadium
```

11.

```sql
SELECT matchid, mdate, COUNT(*)
  FROM game JOIN goal ON matchid = id
 WHERE (team1 = 'POL' OR team2 = 'POL')
GROUP BY matchid, mdate
```

12.

```sql
select matchid, mdate, count(*)
FROM game join goal on matchid = id
where goal.teamid = 'GER'
GROUP BY matchid, mdate
```

13.

```sql
SELECT mdate,
  team1,   
  SUM(CASE WHEN teamid=team1 THEN 1 ELSE 0 END) score1,
  team2,
  SUM(CASE WHEN teamid=team2 THEN 1 ELSE 0 END) score2
  FROM game  JOIN goal ON matchid = id
GROUP BY mdate, team1, team2
```

### Movies

1.

```sql
SELECT id, title
 FROM movie
 WHERE yr=1962
```

2.

```sql
SELECT yr
   FROM movie
   WHERE title = 'Citizen Kane'
```

3.

```sql
SELECT id, title, yr
   FROM movie
   WHERE title LIKE '%Star Trek%'
   ORDER BY yr
```

4.

```sql
SELECT title
  FROM movie
  WHERE id IN ('11768', '11955', '21191')
```

5.

```sql
SELECT id
  FROM actor
  WHERE name = 'Glenn Close'
```

6.

```sql
SELECT id
  FROM movie
  WHERE title = 'Casablanca'
```

7.

```sql
SELECT actor.name
  FROM movie JOIN casting
                                  ON movie.id = casting.movieid
                        JOIN actor         
                                 ON casting.actorid = actor.id
  WHERE movie.title = 'Casablanca'
```

8.

```sql
SELECT actor.name
  FROM movie JOIN casting
                                  ON movie.id = casting.movieid
                        JOIN actor         
                                 ON casting.actorid = actor.id
  WHERE movie.title = 'Alien'
```

9.

```sql
SELECT movie.title
  FROM movie JOIN casting
                                  ON movie.id = casting.movieid
                        JOIN actor         
                                 ON casting.actorid = actor.id
  WHERE actor.name = 'Harrison Ford'
```

10.

```sql
SELECT movie.title
  FROM movie JOIN casting
                                  ON movie.id = casting.movieid
                        JOIN actor         
                                 ON casting.actorid = actor.id
  WHERE actor.name = 'Harrison Ford' AND casting.ord != 1
```

11.

```sql
SELECT movie.title, actor.name
   FROM movie JOIN casting
                         ON movie.id = casting.movieid
              JOIN actor
                         ON casting.actorid = actor.id
          WHERE movie.yr = 1962 AND casting.ord = 1
```

12.

```sql
SELECT yr, COUNT(title) FROM
  movie JOIN casting ON movie.id=movieid
         JOIN actor   ON actorid=actor.id
WHERE name='John Travolta'
GROUP BY yr
HAVING COUNT(title)=(SELECT MAX(c) FROM
(SELECT yr,COUNT(title) AS c FROM
   movie JOIN casting ON movie.id=movieid
         JOIN actor   ON actorid=actor.id
 WHERE name='John Travolta'
 GROUP BY yr) AS t
)
```

13.

```sql
SELECT movie.title, actor.name FROM actor
       JOIN casting ON actor.id = casting.actorid
       JOIN movie ON casting.movieid = movie.id
      WHERE casting.ord = 1 AND casting.movieid IN (
			SELECT casting
			WHERE actorid IN (
			  SELECT id FROM actor
			  WHERE name='Julie Andrews'))
```

14.

```sql
SELECT actor.name
  FROM actor
  JOIN casting ON actor.id = actorid
    WHERE casting.ord = 1
  GROUP BY actor.name
    HAVING COUNT(*) >= 30
```

15.

```sql
SELECT movie.title, COUNT(actorid)
  FROM casting JOIN movie ON movieid = movie.id
  WHERE movie.yr = 1978
  GROUP BY movie.title
  ORDER BY 2 DESC
```

16.

```sql
SELECT DISTINCT name FROM actor
where id IN
(SELECT actorid
FROM movie JOIN casting
ON movie.id=movieid
JOIN actor ON actor.id=movieid
where movie.id
 IN
(SELECT movieid
  FROM actor JOIN casting
    ON actor.id = actorid
  WHERE actor.name = 'Art Garfunkel'))
AND name !='Art Garfunkel'
```

or

```sql
SELECT DISTINCT d.name
FROM actor d JOIN casting a ON (a.actorid=d.id)
   JOIN casting b ON (a.movieid=b.movieid)
   JOIN actor c ON (b.actorid=c.id
                AND c.name='Art Garfunkel')
  WHERE d.id!=c.id
```
### Sum & Count

1.

```sql
SELECT SUM(population)
	FROM world
```

2.

```sql
select DISTINCT continent FROM world
```

3.

```sql
SELECT SUM(GDP) FROM world
	WHERE continent = 'Africa'
```

4.

```sql
SELECT COUNT(name) from world
where area > 1000000
```

5.

```sql
select sum(population) from world
where name IN ('France','Germany','Spain')
```

6.

```sql
SELECT continent, count(name) from world
group by continent
```

7.

```sql
select continent, count(name) from world
where population >= 10000000
GROUP BY continent
```

8.

```sql
select continent from world
group by continent
having sum(population) > 100000000
```

# Subqueries

### SELECT within SELECT

1.

```sql
SELECT name FROM world
  WHERE population >
     (SELECT population FROM world
      WHERE name='Russia')
```

2.

```sql
SELECT name
FROM world
  WHERE continent = 'Europe' AND gdp / population >
     (SELECT gdp / population FROM world
      WHERE name='United Kingdom')
```

3.

```sql
SELECT name, continent FROM world 
WHERE continent IN (SELECT continent FROM world WHERE name = 'Australia' OR name = 'Argentina') 
ORDER BY name
```

4.

```sql
select name, population from world
where population > (SELECT population FROM world where name = 'Canada') AND 
population < (SELECT population FROM world WHERE name = 'Poland')
```

5.

```sql
select name, CONCAT(ROUND(100 * population / (SELECT population FROM world WHERE name = 'Germany')), '%')
FROM world
WHERE continent = 'Europe'
```

6.

```sql
select name from world
WHERE gdp > ALL(select gdp from world where continent = 'Europe' AND gdp IS NOT NULL)
```

7.

```sql
SELECT continent, name, area FROM world x
  WHERE area >= ALL
    (SELECT area FROM world y
        WHERE y.continent=x.continent
          AND area>0)
```

8.

```sql
SELECT continent, name FROM world x
   WHERE name = (SELECT name FROM world y WHERE x.continent = y.continent ORDER BY name ASC LIMIT 1)
```

9.

```sql
SELECT name, continent, population FROM world x
WHERE 25000000 > ALL(SELECT population FROM world y
                                WHERE x.continent = y.continent) 
```

10.

```sql
SELECT name, continent FROM world x
   WHERE population > ALL(SELECT population * 3 FROM world y WHERE x.continent = y.continent AND x.name != y.name)
```

### NULL, Innter JOIN, LET JOIN, RIGHT JOIN

1.

```sql
SELECT name FROM teacher
WHERE dept IS NULL
```

2.

```sql
SELECT teacher.name, dept.name
 FROM teacher INNER JOIN dept
           ON (teacher.dept=dept.id)
```

3.

```sql
SELECT teacher.name, dept.name
 FROM teacher LEFT JOIN dept
           ON (teacher.dept=dept.id)
```

4.

```sql
SELECT teacher.name, dept.name
 FROM teacher RIGHT JOIN dept
           ON (teacher.dept=dept.id)
```

5.

```sql
SELECT name, COALESCE(mobile,'07986 444 2266') AS mobiley FROM teacher
```

6.

```sql

```

7.

```sql

```