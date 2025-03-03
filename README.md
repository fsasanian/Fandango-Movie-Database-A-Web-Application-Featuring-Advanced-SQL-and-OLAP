# Fandango-Movie-Database-A-Web-Application-Featuring-Advanced-SQL-and-OLAP
https://www.loom.com/share/a25310366a654082ac3136201fa94602?sid=cafd2c49-51fe-47e8-85fe-8f8a4834dba6
# Fandango: A Comprehensive Movie Database Web App with Advanced SQL, OLAP, and a User-Friendly Interface
Fandango is a web application designed to manage movie data while showcasing a range of complex SQL queries, including set operations, set membership, set comparison, subqueries using the WITH clause, advanced aggregate functions, and OLAP. The application features a user-friendly interface with interactive menus, buttons, and icons.


## Features-----------------------------------------------------------------
- **Advanced SQL Queries:** Advanced SQL queries including (set operations, set membership, comparison, and subqueries with the WITH clause).
- **OLAP Functionality:** OLAP functionality including window functions and ROLLUP.
- **User-Friendly Interface:** A userfriendly interface with Bootstrap-based menus, buttons, and icons ,and Creating interactive charts and visualizations using Chart.js.
- **User Authentication:** Registration, login, and logout functionality using Flask-Login.
- **Robust Error Handling:** Custom error pages for 404 and 500 errors, and Logging of important events and errors in `app.log`.


## How to Set it Up-----------------------------------------------------------
1. **Install:** Python, MySQL, Flask.
2. **Run the app** by typing in terminal: `/opt/anaconda3/bin/python app1.py`
3. **Open the browser** and go to [http://127.0.0.1:5000/](http://127.0.0.1:5000/)


## Advanced SQL Query Documentation--------------------------------------------

### High Rated Reviews
**query:**

WITH HighRatings AS (
    SELECT * FROM Review WHERE Rating >= 4
)
SELECT * FROM HighRatings;
**This query uses a Common Table Expression (CTE) with the WITH clause to select all reviews that have a rating of 4 or higher.**
-------------------------------

### Average Rating per Movie

SELECT MovieID, AVG(Rating) AS AvgRating
FROM Review
GROUP BY MovieID;
**This query calculates the average rating for each movie by grouping the reviews by MovieID and using the AVG() aggregate function.**
-----------------------------------

### Movie Detail with Reviews

**Movie Details:** SELECT * FROM Movie WHERE MovieID = %s;

**Movie Revies:** SELECT * FROM Review WHERE MovieID = %s ORDER BY ReviewDate DESC;

**The first query show the details for a specific movie. The second query fetches all reviews for that movie, ordered by the most recent review first.**
------------------------------------------

### Movies Above Overall Average Rating

SELECT MovieID, AVG(Rating) AS AvgRating 
FROM Review 
GROUP BY MovieID 
HAVING AVG(Rating) > (SELECT AVG(Rating) FROM Review);

**This query first calculates the overall average rating across all reviews using a subquery. Then, it selects movies whose average rating is higher than that overall average**
--------------------------------------------------
### Ranked Movies (OLAP)
SELECT 
    MovieID, 
    AVG(Rating) AS AvgRating,
    RANK() OVER (ORDER BY AVG(Rating) DESC) AS rank_val
FROM Review
GROUP BY MovieID
ORDER BY rank_val;


**This query calculates the average rating per movie and then uses the window function RANK() to assign a rank based on the average rating.**
-------------------------------------------------------

### Movies by Genre (Set Membership)

SELECT * FROM Movie WHERE Genre IN ('Comedy', 'Action', 'Drama');

**This query uses the IN operator to filter movies that belong to one of the specified genres (Comedy, Action, or Drama).**
---------------------------------------------------------

### Movies (Comedy/Action) Using Set Operations

(SELECT * FROM Movie WHERE Genre = 'Comedy')
UNION
(SELECT * FROM Movie WHERE Genre = 'Action');

**This query combines movies from the Comedy and Action genres.**
-----------------------------------

### ROLLUP for Review Summary

SELECT 
    m.Genre,
    COUNT(*) AS TotalReviews,
    AVG(r.Rating) AS AverageRating
FROM Movie m
JOIN Review r ON m.MovieID = r.MovieID
GROUP BY m.Genre WITH ROLLUP;

**This query summarizes review data by genre with a grand total row.**
------------------------------------------

### Search Movies by Title

SELECT * FROM Movie WHERE Title LIKE %s;

**This query searches for movies by title.** 
---------------------------------------------

### Submit a Review

INSERT INTO Review (MovieID, Rating, Comment, ReviewDate, UserID) VALUES (%s, %s, %s, NOW(), %s);

**This query inserts a new review into the Review table.**
----------------------------------------------

### View All Reviews

SELECT * FROM Review ORDER BY ReviewDate DESC;

**This query retrieves all reviews from the Review table, ordered by review date in descending order**


## User Interface and Interactive Elements------------------------------------------

**Home Page:**  
The home page features a navigation bar with links to key sections like Movies Above Average, Ranked Movies, and Movies by Genre.

**Movie Detail Page:**  
Displays detailed information about a selected movie, including its title, genre, synopsis, and reviews. Includes a Back to Home button for easy navigation.

**Review Submission:**  
A form that allows users to submit reviews for a movie, with input fields for movie ID, rating, and comment.
  
**Interactive Charts:**  
Useing Chart.js to display visual data on pages like the Ranked Movies page.

**Search:**  
A search box on the home page allows users to enter a movie title and click "Search" to find movies by title.

**Error Handling:**
Custom error pages (404 and 500) provide user-friendly messages, and detailed logs are saved in app.log for troubleshooting.


# Troubleshooting and FAQ----------------------------------------

- **Database Errors:** Ensure my MySQL credentials in `app1.py` are correct.
- **Application Not Starting:** Verify that all dependencies are installed and using the correct Python interpreter.
- **Login Issues:** Ensure that email addresses are entered correctly (with an "@" symbol).
- **Examples:**
 **Problem:** I can’t see the movies.  
  **Solution:** Check the database settings and make sure MySQL is running.
  
- **Problem:** The login page is not working.  (Put the example in Screenshot file)
  **Solution:** Check that the typed  email correctly (it should have an "@" sign) and try again. 
  

