
# Fandango Movie Database & Analytics

A movie database web application built with Python, Flask,
and MySQL to demonstrate advanced SQL querying, OLAP
operations, database management, and interactive data
visualization.

## Project Demo

[Watch the Application Demo on Loom](https://www.loom.com/share/a25310366a654082ac3136201fa94602)

## Project Overview

This project explores how relational databases and
advanced SQL techniques can support data-driven
applications.

The Fandango application was designed to allow users
to browse movies, search by title, view movie reviews,
submit ratings, and explore movie analytics.

The project emphasizes:

- Relational database querying with MySQL
- Advanced SQL analytics and Common Table Expressions
- Window functions and OLAP operations
- Web application development using Flask
- Interactive data visualization with Chart.js

## Technologies Used

| Category | Technologies |
|---|---|
| Programming | Python, SQL |
| Database | MySQL |
| Web Framework | Flask |
| Authentication | Flask-Login |
| Frontend | HTML, Bootstrap |
| Visualization | Chart.js |
| Analytics | CTEs, Subqueries, Window Functions, ROLLUP |

## Key Features

### Movie Management and Search
- Browse available movies and their details.
- Search for movies using partial title matches.
- View associated ratings and reviews.
- Submit movie ratings and reviews.

### Advanced SQL Analytics
- Common Table Expressions (CTEs)
- Aggregate functions and grouped summaries
- Subqueries and set operations
- Set membership filtering
- Ranking with SQL window functions
- OLAP summaries using ROLLUP

### Web Application
- User registration, login, and logout
- Bootstrap-based navigation
- Interactive charts using Chart.js
- Custom 404 and 500 error pages
- Application logging for troubleshooting

## SQL Query Examples

The following queries demonstrate the main analytical
techniques documented in this project.

### 1. High-Rated Reviews — CTE

```sql
WITH HighRatings AS (
    SELECT *
    FROM Review
    WHERE Rating >= 4
)
SELECT *
FROM HighRatings;
```

Uses a Common Table Expression to retrieve reviews
with ratings of 4 or higher.

### 2. Average Rating per Movie — Aggregation

```sql
SELECT
    MovieID,
    AVG(Rating) AS AvgRating
FROM Review
GROUP BY MovieID;
```

Calculates the average review rating for each movie.

### 3. Movie Details and Reviews

```sql
SELECT *
FROM Movie
WHERE MovieID = %s;

SELECT *
FROM Review
WHERE MovieID = %s
ORDER BY ReviewDate DESC;
```

Retrieves the selected movie's information and its
reviews, ordered from newest to oldest.

The `%s` placeholders are intended for parameterized
queries executed through Python.

### 4. Movies Above Overall Average Rating — Subquery

```sql
SELECT
    MovieID,
    AVG(Rating) AS AvgRating
FROM Review
GROUP BY MovieID
HAVING AVG(Rating) > (
    SELECT AVG(Rating)
    FROM Review
);
```

Identifies movies whose average rating is higher
than the overall average across all reviews.

### 5. Ranked Movies — Window Function

```sql
SELECT
    MovieID,
    AVG(Rating) AS AvgRating,
    RANK() OVER (
        ORDER BY AVG(Rating) DESC
    ) AS rank_val
FROM Review
GROUP BY MovieID
ORDER BY rank_val;
```

Ranks movies according to their average ratings
using the SQL `RANK()` window function.

### 6. Movies by Genre — Set Membership

```sql
SELECT *
FROM Movie
WHERE Genre IN ('Comedy', 'Action', 'Drama');
```

Filters the database to display movies belonging
to selected genres.

### 7. Movies by Genre — Set Operations

```sql
SELECT *
FROM Movie
WHERE Genre = 'Comedy'

UNION

SELECT *
FROM Movie
WHERE Genre = 'Action';
```

Combines results from Comedy and Action genres
using SQL `UNION`.

### 8. Review Summary by Genre — OLAP ROLLUP

```sql
SELECT
    m.Genre,
    COUNT(*) AS TotalReviews,
    AVG(r.Rating) AS AverageRating
FROM Movie m
JOIN Review r
    ON m.MovieID = r.MovieID
GROUP BY m.Genre WITH ROLLUP;
```

Produces aggregated review statistics by genre,
including a grand-total row.

### 9. Search Movies by Title

```sql
SELECT *
FROM Movie
WHERE Title LIKE %s;
```

Supports searching for movies by title through
a parameterized query.

### 10. Submit a Movie Review

```sql
INSERT INTO Review (
    MovieID,
    Rating,
    Comment,
    ReviewDate,
    UserID
)
VALUES (%s, %s, %s, NOW(), %s);
```

Adds a new user review to the database.

### 11. View All Reviews

```sql
SELECT *
FROM Review
ORDER BY ReviewDate DESC;
```

Retrieves all reviews, beginning with the most recent.

## User Interface

The application includes several interactive components:

**Home Page:** Navigation to movie categories,
rating analytics, and database features.

**Movie Details:** Individual movie information,
ratings, and associated reviews.

**Search:** Title-based movie search functionality.

**Review Submission:** Forms for submitting movie
ratings and comments.

**Visual Analytics:** Interactive charts created
using Chart.js.

**Authentication:** User registration, login,
and logout functionality.

**Error Handling:** Custom error pages and
application logging.

## Running the Application

The current public repository contains project
documentation and SQL examples. The original Flask
application files and database setup materials
have not yet been uploaded.

Once the source files are available, this section
will include complete installation instructions,
database initialization steps, and dependencies.

The original application documentation refers to
`app1.py` as the Python entry point and uses
`http://127.0.0.1:5000/` as its local address.

## Troubleshooting

**Database connection issues**
- Confirm that MySQL is running.
- Verify the database connection settings.

**Application startup issues**
- Confirm that the required Python packages
  are installed.

**Login issues**
- Check that the registration and login
  information is entered correctly.

**Missing movie data**
- Verify the database connection and
  confirm that the tables contain records.

## Future Improvements

- Upload the original Flask application source.
- Add database schema and sample data.
- Document installation dependencies.
- Include application screenshots.
- Add reproducible database setup instructions.

## Author

**Farnaz Sasanian**

M.S. in Data Science — Illinois Institute of Technology

[GitHub](https://github.com/fsasanian) |
[LinkedIn](https://www.linkedin.com/in/fsasanian/) |
[Tableau Portfolio](https://public.tableau.com/app/profile/farnaz.sasanian/vizzes)
