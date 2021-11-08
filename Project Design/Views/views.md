# Views
## View 1
Who are the main actors in our movies?
```
CREATE OR REPLACE VIEW actorjobs 
AS SELECT worksfor.MovieID,actor.ActorID,actor.Fname,actor.Lname,movie.Title 
FROM actor 
INNER JOIN worksfor 
ON worksfor.ActorID=actor.ActorID 
INNER JOIN movie 
ON worksfor.MovieID=movie.MovieID;
```
![View 1](https://github.com/Abbas-Rizvi/Movie-Knight/blob/master/Project%20Design/Views/images/View1.png)

## View 2
How many actors are above 50 years old, grouped by gender?
```
CREATE OR REPLACE VIEW agegap
SELECT COUNT(ActorID) AS Count,Sex 
FROM actor 
WHERE actor.age = ANY(SELECT Age FROM actor WHERE Age > 50) 
GROUP BY Sex;
```
![View 2](https://github.com/Abbas-Rizvi/Movie-Knight/blob/master/Project%20Design/Views/images/View2.png)

## View 3
First create a view that displays average age.
```
CREATE VIEW averageage AS 
SELECT AVG(Cast(Age as INTEGER)) AS 'Average Age' 
FROM totalage;
```
Then we make correlated nested query
```

```

## View 5
What are the ages of all directors and actors?
```
CREATE VIEW totalage AS 
SELECT Age FROM actor 
UNION 
SELECT Age 
FROM director 
ORDER BY Age;
```
![View 5](https://github.com/Abbas-Rizvi/Movie-Knight/blob/master/Project%20Design/Views/images/View5.png)

## View 6
What are the genres for each film?
```
CREATE VIEW moviegenre AS 
SELECT movie.Title,genre.GName 
FROM movie 
INNER JOIN genre 
ON movie.GName = genre.GName;
```
![View 6](https://github.com/Abbas-Rizvi/Movie-Knight/blob/master/Project%20Design/Views/images/View6.png)

## View 7
What is the rating score for each film?
```
CREATE OR REPLACE VIEW movierating AS 
SELECT movie.Title,rating.Rating 
FROM movie 
INNER JOIN rating 
ON movie.RateNo = rating.RateNo;
```
![View 7](https://github.com/Abbas-Rizvi/Movie-Knight/blob/master/Project%20Design/Views/images/View7.png)

## View 8
Which Director's win the award for longest Film by running time?
```
CREATE VIEW timeaward AS
SELECT director.Fname, director.Lname,movie.Length 
FROM director 
INNER JOIN movie 
ON director.DirectorID = movie.DirectorID 
GROUP BY movie.Length;
```
![View 8](https://github.com/Abbas-Rizvi/Movie-Knight/blob/master/Project%20Design/Views/images/View8.png)

## View 9
What is an actor's rating for a film?
```
SELECT actorjobs.MovieID,actorjobs.Fname,actorjobs.Lname, rating.Rating 
FROM actorjobs 
INNER JOIN rating 
ON rating.RateNo = actorjobs.MovieID;
```
![View 9](https://github.com/Abbas-Rizvi/Movie-Knight/blob/master/Project%20Design/Views/images/View9.png)

## View 10
What is the average rating of our movies?
```
SELECT AVG(Cast(Rating AS INTEGER)) 
AS 'AverageRating' 
FROM rating;
```
![View 10](https://github.com/Abbas-Rizvi/Movie-Knight/blob/master/Project%20Design/Views/images/View10.png)
