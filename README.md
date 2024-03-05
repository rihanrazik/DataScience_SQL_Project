# SQL_Project for Data Science certification
**FinalProject_for_SQL for Data Science certification**

**Comprehensive SQL data analysis project based on the Yelp database, intended for a SQL Data Science certification.** 

**INTRO:**
Data Scientist Role Play: Profiling and Analyzing the Yelp Dataset Coursera Worksheet

This is a 2-part assignment. In the first part, you are asked a series of questions that will help you profile and understand the data just like a data scientist would. For this first part of the assignment, you will be assessed both on the correctness of your findings, as well as the code you used to arrive at your answer. You will be graded on how easy your code is to read, so remember to use proper formatting and comments where necessary.

In the second part of the assignment, you are asked to come up with your own inferences and analysis of the data for a particular research question you want to answer. You will be required to prepare the dataset for the analysis you choose to do. As with the first part, you will be graded, in part, on how easy your code is to read, so use proper formatting and comments to illustrate and communicate your intent as required.

For both parts of this assignment, use this "worksheet." It provides all the questions you are being asked, and your job will be to transfer your answers and SQL coding where indicated into this worksheet so that your peers can review your work. You should be able to use any Text Editor (Windows Notepad, Apple TextEdit, Notepad ++, Sublime Text, etc.) to copy and paste your answers. If you are going to use Word or some other page layout application, just be careful to make sure your answers and code are lined appropriately.
In this case, you may want to save as a PDF to ensure your formatting remains intact for you reviewer.

**QUESTIONS:**

**PART 1:** 
**Yelp Dataset Profiling and Understanding**

**1. Profile the data by finding the total number of records for each of the tables below:**
	
i. Attribute table =10000
SELECT count(*) FROM attribute;

ii. Business table = 10000
SELECT count(*) FROM business;

iii. Category table = 10000
SELECT count(*) FROM category;

iv. Checkin table = 10000
SELECT count(*) FROM checkin;
-------------------------------------------------------------
**2. Are there any columns with null values in the Users table? Indicate "yes," or "no."**

	Answer: no.
	
	**
	SQL code used to arrive at answer:**

SELECT
    CASE
        WHEN COUNT(*) > 0 THEN 'yes,'
        ELSE 'no.'
    END AS any_null_values
FROM
    User
WHERE
    id IS NULL OR
    name IS NULL OR
    review_count IS NULL OR
    yelping_since IS NULL OR
    useful is NULL or
    funny is NULL or
    cool is NULL or
    fans is NULL or 
    average_stars is NULL or
    compliment_hot is NULL or
    compliment_more is NULL or 
    compliment_profile is NULL or
    compliment_cute is NULL or
    compliment_list is NULL or
    compliment_note is NULL or
    compliment_plain is NULL or
    compliment_cool is NULL or
    compliment_funny  is NULL or
    compliment_writer is NULL or
    compliment_photos  is NULL;

--------------------------------------------
**3. For each table and column listed below, display the smallest (minimum), largest (maximum), and average (mean) value for the following fields:**

	i. Table: Review, Column: Stars
	
		min:1		max:5		avg:3.7082
	
		SELECT min(stars), max(stars), avg(stars)
		FROM review;	
	
	ii. Table: Business, Column: Stars
	
		min:1.0		max:5.0		avg:3.7082
	
		SELECT min(stars), max(stars), avg(stars)
		FROM business;
		
	
	iii. Table: Tip, Column: Likes
	
		min:0		max:2		avg:0.0144
		
		SELECT min(likes), max(likes), avg(likes)
		FROM tip;
	
	iv. Table: Checkin, Column: Count
	
		min:1		max:53		avg:1.9414
		
		SELECT min(count), max(count), avg(count)
		FROM checkin;
	
	v. Table: User, Column: Review_count
	
		min:0		max:2000	avg:24.2995

		SELECT min(Review_count), max(Review_count), avg(Review_count)
		FROM user;		
-------------------------------------------------
**5. List the cities with the most reviews in descending order:**

SQL code used to arrive at answer:

SELECT city, count(Review_count) as Number_of_Reviews
FROM business
GROUP BY city
ORDER BY Number_of_Reviews DESC;

	Copy and Paste the Result Below:
+-----------------+-------------------+
| city            | Number_of_Reviews |
+-----------------+-------------------+
| Las Vegas       |              1561 |
| Phoenix         |              1001 |
| Toronto         |               985 |
| Scottsdale      |               497 |
| Charlotte       |               468 |
| Pittsburgh      |               353 |
| Montréal        |               337 |
| Mesa            |               304 |
| Henderson       |               274 |
| Tempe           |               261 |
| Edinburgh       |               239 |
| Chandler        |               232 |
| Cleveland       |               189 |
| Gilbert         |               188 |
| Glendale        |               188 |
| Madison         |               176 |
| Mississauga     |               150 |
| Stuttgart       |               141 |
| Peoria          |               105 |
| Markham         |                80 |
| Champaign       |                71 |
| North Las Vegas |                70 |
| North York      |                64 |
| Surprise        |                60 |
| Richmond Hill   |                54 |
+-----------------+-------------------+
(Output limit exceeded, 25 of 362 total rows shown)

-------------------------------------------------------
**6. Find the distribution of star ratings to the business in the following cities:**

**i. Avon**

SQL code used to arrive at answer:

SELECT avg(stars) AS Star_Rating, count(stars) AS count
FROM business
WHERE city = "Avon";

Copy and Paste the Resulting Table Below (2 columns â€“ star rating and count):
+-------------+-------+
| Star_Rating | count |
+-------------+-------+
|        3.45 |    10 |
+-------------+-------+

**ii. Beachwood**

SQL code used to arrive at answer:

SELECT round(avg(stars),2) AS Star_Rating, count(stars) AS count
FROM business
WHERE city = "Beachwood";

Copy and Paste the Resulting Table Below (2 columns â€“ star rating and count):
+-------------+-------+
| Star_Rating | count |
+-------------+-------+
|        3.96 |    14 |
+-------------+-------+	

-----------------------------------------
**7. Find the top 3 users based on their total number of reviews:**

SQL code used to arrive at answer:

SELECT name, count(review_count) as Total_number_of_reviews
FROM user
GROUP BY name
ORDER BY Total_number_of_reviews desc
LIMIT 3;	
		
	Copy and Paste the Result Below:
+-------+-------------------------+
| name  | Total_number_of_reviews |
+-------+-------------------------+
| John  |                     102 |
| David |                      90 |
| Chris |                      74 |
+-------+-------------------------+		
-------------------------------------------------------------
**8. Does posing more reviews correlate with more fans?**
No! 
Based on my findings, having more reviews does not correlate with having more fans. 
I used the SQL query below to assess this question, but the results show that users with the highest 
number of followers do not necessarily have the highest number of reviews. In fact, there are users 
with less fans, but they have more reviews than users with the highest number of fans.

	Please explain your findings and interpretation of the results:
	
--SQL code test1:
SELECT name, sum(fans) as numfans, count(review_count) as reviews
FROM user
GROUP BY name
ORDER BY numfans  des;

Result:
+-----------+---------+---------+
| name      | numfans | reviews |
+-----------+---------+---------+
| Amy       |     519 |      35 |
| Mimi      |     498 |       5 |
| Harald    |     311 |       2 |
| Gerald    |     256 |       2 |
| Lisa      |     207 |      58 |
| Nicole    |     200 |      35 |
| Christine |     187 |      23 |
| Mark      |     156 |      59 |
| Jen       |     148 |      32 |
| Linda     |     148 |      26 |
| William   |     142 |      21 |
| Cat       |     133 |       5 |
| Michelle  |     133 |      43 |
| Tiffany   |     128 |      21 |
| Fran      |     126 |       3 |
| Karen     |     123 |      40 |
| Christina |     120 |      22 |
| Lissa     |     120 |       2 |
| Mike      |     119 |      74 |
| Jessica   |     116 |      45 |
| Andrew    |     114 |      41 |
| Ben       |     112 |      16 |
| bernice   |     105 |       1 |
| Melissa   |     104 |      58 |
| Roanna    |     104 |       1 |
+-----------+---------+---------+
(Output limit exceeded, 25 of 3454 total rows shown)

--SQL code test2:
SELECT name, sum(fans) as numfans, count(review_count) as reviews
FROM user
GROUP BY name
ORDER BY reviews  desc; 

Result:
| name     | numfans | reviews |
+----------+---------+---------+
| John     |      46 |     102 |
| David    |      25 |      90 |
| Chris    |      52 |      74 |
| Mike     |     119 |      74 |
| Michael  |      34 |      72 |
| Jennifer |      86 |      63 |
| Mark     |     156 |      59 |
| Lisa     |     207 |      58 |
| Melissa  |     104 |      58 |
| Sarah    |     100 |      55 |
| Alex     |      22 |      54 |
| James    |      86 |      48 |
| Jessica  |     116 |      45 |
| Ryan     |      24 |      45 |
| J        |      13 |      43 |
| Michelle |     133 |      43 |
| Andrew   |     114 |      41 |
| Kevin    |      20 |      41 |
| Mary     |      18 |      41 |
| Amanda   |      26 |      40 |
| Ashley   |      16 |      40 |
| Brian    |      72 |      40 |
| Karen    |     123 |      40 |
| Laura    |      38 |      39 |
| Robert   |       9 |      39 |
+----------+---------+---------+
(Output limit exceeded, 25 of 3454 total rows shown)


In conclusion, posing more reviews does not correlate with having more fans.
----------------------------------------

**9. Are there more reviews with the word "love" or with the word "hate" in them?**

 Answer:

There are more review with the word "love" compared to the word "hate". I have tested it with the followint querry.
	
	SQL code used to arrive at answer:
 
--Test1:
SELECT count(*)
FROM review
WHERE text like "%love%" 	;

Result:
+----------+
| count(*) |
+----------+
|     1780 |
+----------+

--Test2:
SELECT count(*)
FROM review
WHERE text like "%hate%";

Result:
+----------+
| count(*) |
+----------+
|      232 |
+----------+

The word "love" was used 1780 times in the reviews. But, the word "hate" was only used 232 times in the reviews.
Therefore, we can conclude that there are more review with the word "love". 

------------------------------------------------------

**10. Find the top 10 users with the most fans:**

	SQL code used to arrive at answer:

SELECT name, sum(fans) as numfans
FROM user
GROUP BY name
ORDER BY numfans  desc 
LIMIT 10;	
	
	Copy and Paste the Result Below:

+-----------+---------+
| name      | numfans |
+-----------+---------+
| Amy       |     519 |
| Mimi      |     498 |
| Harald    |     311 |
| Gerald    |     256 |
| Lisa      |     207 |
| Nicole    |     200 |
| Christine |     187 |
| Mark      |     156 |
| Jen       |     148 |
| Linda     |     148 |
+-----------+---------+
	
------------------------------------------------------
------------------------------------------------------
**PART 2:**
**Inferences and Analysis**

**1. Pick one city and category of your choice and group the businesses in that city or category by their overall star rating. Compare the businesses with 2-3 stars to the businesses with 4-5 stars and answer the following questions. Include your code.**
	
First, I will use the following SQL code to extract the data I am looking for to select the businesses and group them by starratings as "Group1" and "Group2":

SELECT 
CASE
    WHEN b.stars between 2.0 and 3.0 THEN "Group1"
    ELSE "Group2"
END AS "Group",
b.name as BusinessName, b.stars As StarRating, b.city as City,c.category 
FROM business b JOIN category c ON 
b.id = c.business_id
WHERE city = "Toronto" and c.category = "Restaurants" and StarRating between 2 and 5
GROUP BY BusinessName, "Group"
ORDER BY StarRating  ASC;

Result:
+--------+--------------------+------------+---------+-------------+
| Group  | BusinessName       | StarRating | City    | category    |
+--------+--------------------+------------+---------+-------------+
| Group1 | 99 Cent Sushi      |        2.0 | Toronto | Restaurants |
| Group1 | Big Smoke Burger   |        3.0 | Toronto | Restaurants |
| Group1 | Pizzaiolo          |        3.0 | Toronto | Restaurants |
| Group2 | The Kosher Gourmet |        3.5 | Toronto | Restaurants |
| Group2 | Edulis             |        4.0 | Toronto | Restaurants |
| Group2 | Mama Mia           |        4.0 | Toronto | Restaurants |
| Group2 | Naniwa-Taro        |        4.0 | Toronto | Restaurants |
| Group2 | Cabin Fever        |        4.5 | Toronto | Restaurants |
| Group2 | Sushi Osaka        |        4.5 | Toronto | Restaurants |
+--------+--------------------+------------+---------+-------------+

-----------------------------------------------------------------------------

**i. Do the two groups you chose to analyze have a different distribution of hours?**

Yes the two groups have different distribution of hours. See below:

SELECT 
CASE
    WHEN b.stars between 2.0 and 3.0 THEN "Group1"
    ELSE "Group2"
END AS "Group",
b.name as BusinessName, b.stars As StarRating, b.city as City,c.category, h.hours 
FROM business b JOIN category c ON 
b.id = c.business_id
JOIN hours h on
b.id=h.business_id
WHERE city = "Toronto" and c.category = "Restaurants" and StarRating between 2 and 5
GROUP BY BusinessName, "Group"
ORDER BY StarRating  ASC;

+--------+------------------+------------+---------+-------------+----------------------+
| Group  | BusinessName     | StarRating | City    | category    | hours                |
+--------+------------------+------------+---------+-------------+----------------------+
| Group1 | 99 Cent Sushi    |        2.0 | Toronto | Restaurants | Saturday|11:00-23:00 |
| Group1 | Big Smoke Burger |        3.0 | Toronto | Restaurants | Saturday|10:30-21:00 |
| Group1 | Pizzaiolo        |        3.0 | Toronto | Restaurants | Saturday|10:00-4:00  |
| Group2 | Edulis           |        4.0 | Toronto | Restaurants | Saturday|18:00-23:00 |
| Group2 | Cabin Fever      |        4.5 | Toronto | Restaurants | Saturday|16:00-2:00  |
| Group2 | Sushi Osaka      |        4.5 | Toronto | Restaurants | Saturday|11:00-23:00 |
+--------+------------------+------------+---------+-------------+----------------------+

-----------------------------------------------------------------------------
**ii. Do the two groups you chose to analyze have a different number of reviews?**

Yes. Number of review vary between these businesses. lowest number of review being 5 (average 2.0 review) and the highest number of review being 89 (average 4.0 review). See below for query and result.
         
SELECT 
CASE
    WHEN b.stars between 2.0 and 3.0 THEN "Group1"
    ELSE "Group2"
END AS "Group",
b.name as BusinessName, 
b.stars As StarRating, 
b.city as City, c.category, 
h.hours,
count(b.review_count) as NumberofReviews
FROM business b JOIN category c ON 
b.id = c.business_id
JOIN hours h on
b.id=h.business_id
WHERE city = "Toronto" and c.category = "Restaurants" 
GROUP BY BusinessName, "Group"
ORDER BY StarRating  ASC;

Result:     
+--------+------------------+------------+---------+-------------+----------------------+-----------------+
| Group  | BusinessName     | StarRating | City    | category    | hours                | NumberofReviews |
+--------+------------------+------------+---------+-------------+----------------------+-----------------+
| Group1 | 99 Cent Sushi    |        2.0 | Toronto | Restaurants | Saturday|11:00-23:00 |              77 |
| Group1 | Big Smoke Burger |        3.0 | Toronto | Restaurants | Saturday|10:30-21:00 |              47 |
| Group1 | Pizzaiolo        |        3.0 | Toronto | Restaurants | Saturday|10:00-4:00  |             147 |
| Group2 | Edulis           |        4.0 | Toronto | Restaurants | Saturday|18:00-23:00 |             133 |
| Group2 | Cabin Fever      |        4.5 | Toronto | Restaurants | Saturday|16:00-2:00  |              95 |
| Group2 | Sushi Osaka      |        4.5 | Toronto | Restaurants | Saturday|11:00-23:00 |              28 |
+--------+------------------+------------+---------+-------------+----------------------+-----------------+


-----------------------------------------------------

**iii. Are you able to infer anything from the location data provided between these two groups? Explain.**

Restaurants with Business Parking had the highest number of customers providing rating and averaged a star raing of 3.0.

Sushi Oshaka having the highest rating (4.5) only with 28 ratings must be because it is a specialty dinner-only sushi restaurant, has reservations options and also it is away from the busy downtown core resulting in greater custoemer satisfaction.

++--------+------------------+------------+---------+------------------------+-------------+-------------+-------------------------+----------------------+-----------------+
| Group  | BusinessName     | StarRating | City    | neighborhood           | postal_code | category    | name                    | hours                | NumberofReviews |
+--------+------------------+------------+---------+------------------------+-------------+-------------+-------------------------+----------------------+-----------------+
| Group1 | 99 Cent Sushi    |        2.0 | Toronto | Downtown Core          | M5B 2E5     | Restaurants | GoodForKids             | Saturday|11:00-23:00 |              77 |
| Group1 | Big Smoke Burger |        3.0 | Toronto | Downtown Core          | M4B 2L9     | Restaurants | BusinessParking         | Saturday|10:30-21:00 |             147 |
| Group1 | Pizzaiolo        |        3.0 | Toronto | Entertainment District | M5H 1X6     | Restaurants | BusinessParking         | Saturday|10:00-4:00  |             133 |
| Group2 | Edulis           |        4.0 | Toronto | Niagara                | M5V         | Restaurants | BusinessParking         | Saturday|18:00-23:00 |              95 |
| Group2 | Sushi Osaka      |        4.5 | Toronto | Etobicoke              | M9A 1C2     | Restaurants | RestaurantsReservations | Saturday|11:00-23:00 |              28 |
+--------+------------------+------------+---------+------------------------+-------------+-------------+-------------------------+----------------------+-----------------+

SQL code used for analysis:

SELECT 
CASE
    WHEN b.stars between 2.0 and 3.0 THEN "Group1"
    ELSE "Group2"
END AS "Group",
b.name as BusinessName, 
b.stars As StarRating, 
b.city as City, b.neighborhood, b.postal_code, c.category, a.name,
h.hours,
count(b.review_count) as NumberofReviews
FROM business b JOIN category c ON 
b.id = c.business_id
JOIN hours h on
b.id=h.business_id
JOIN attribute a on
a.business_id=b.id
WHERE city = "Toronto" and c.category = "Restaurants" 
GROUP BY BusinessName, "Group"
ORDER BY StarRating  ASC;

--------------------------------------------

**2. Group business based on the ones that are open and the ones that are closed. What differences can you find between the ones that are still open and the ones that are closed? List at least two differences and the SQL code you used to arrive at your answer.**
		

+--------+------------------+------------+---------+------------------------+-------------+-------------+-------------------------+---------+----------------------+-----------------+
| Group  | BusinessName     | StarRating | City    | neighborhood           | postal_code | category    | name                    | is_open | hours                | NumberofReviews |
+--------+------------------+------------+---------+------------------------+-------------+-------------+-------------------------+---------+----------------------+-----------------+
| Group1 | 99 Cent Sushi    |        2.0 | Toronto | Downtown Core          | M5B 2E5     | Restaurants | GoodForKids             |       0 | Saturday|11:00-23:00 |              77 |
| Group1 | Big Smoke Burger |        3.0 | Toronto | Downtown Core          | M4B 2L9     | Restaurants | BusinessParking         |       1 | Saturday|10:30-21:00 |             147 |
| Group1 | Pizzaiolo        |        3.0 | Toronto | Entertainment District | M5H 1X6     | Restaurants | BusinessParking         |       1 | Saturday|10:00-4:00  |             133 |
| Group2 | Edulis           |        4.0 | Toronto | Niagara                | M5V         | Restaurants | BusinessParking         |       1 | Saturday|18:00-23:00 |              95 |
| Group2 | Sushi Osaka      |        4.5 | Toronto | Etobicoke              | M9A 1C2     | Restaurants | RestaurantsReservations |       1 | Saturday|11:00-23:00 |              28 |
+--------+------------------+------------+---------+------------------------+-------------+-------------+-------------------------+---------+----------------------+-----------------+


i. Difference 1:         

99 Cent Sushi is closed and has the lowest rating. This restaurant must've been under performing and eventually closed down.
         
ii. Difference 2:

99 Cent Sushi being GoodforKids did not help the rating factor.         
         
         
SQL code used for analysis:

SELECT 
CASE
    WHEN b.stars between 2.0 and 3.0 THEN "Group1"
    ELSE "Group2"
END AS "Group",
b.name as BusinessName, 
b.stars As StarRating, 
b.city as City, b.neighborhood, b.postal_code, c.category, a.name,b.is_open,
h.hours,
count(b.review_count) as NumberofReviews
FROM business b JOIN category c ON 
b.id = c.business_id
JOIN hours h on
b.id=h.business_id
JOIN attribute a on
a.business_id=b.id
WHERE city = "Toronto" and c.category = "Restaurants" 
GROUP BY BusinessName, "Group", b.is_open
ORDER BY StarRating  ASC;

----------------------------------------------------------------
----------------------------------------------------------------
**PART 3:**
**For this last part of your analysis, you are going to choose the type of analysis you want to conduct on the Yelp dataset and are going to prepare the data for analysis.**

**Ideas for analysis include: Parsing out keywords and business attributes for sentiment analysis, clustering businesses to find commonalities or anomalies between them, predicting the overall star rating for a business, predicting the number of fans a user will have, and so on. These are just a few examples to get you started, so feel free to be creative and come up with your own problem you want to solve. Provide answers, in-line, to all of the following:**

i. Indicate the type of analysis you chose to do:
I will be conducting **sentiment analysis** by parsing out keywords and business attributes.

i. Write 1-2 brief paragraphs on the type of data you will need for your analysis and why you chose that data:
 
For the sentiment analysis, I chose to categorize Yelp reviews into three distinct categories: 'positive_review,' 'negative_review,' and 'average_review,' utilizing text parsing techniques with SQL. The requisite data for this analysis was extracted from the 'business' and 'review' tables in the Yelp dataset, including crucial information like business name, city, stars, and review text. The 'business' table supplied details about each business, including their star ratings, while the 'review' table contained the textual content of the reviews.

In the SQL query provided, I implemented text parsing by incorporating specific keywords in the review text to classify reviews. Reviews were marked as 'positive_review' if the star rating was greater than 5. For reviews with star ratings between 2 and 5, the text parsing conditions included positive keywords such as 'perfect,' 'good,' 'love,' 'amazing,' and more, leading to the categorization as 'positive_review.' Conversely, negative keywords like 'bad,' 'horrible,' 'terrible,' 'annoying,' and others were used to categorize reviews as 'negative_review.' The 'TypeofReview' column captured the results of this text parsing, providing a clear distinction between positive, negative, and average reviews. This SQL-based approach, integrating your specified text parsing conditions, ensured a detailed sentiment analysis by considering both star ratings and the textual content of the reviews.

iii. Provide the SQL code you used to create your final dataset:

SELECT
    b.name,
    b.city,
    b.stars,
    CASE
        WHEN b.stars >= "4" THEN 'positive_review'
        WHEN b.stars <= "2" THEN 'Negative_review'
        WHEN r.text LIKE '%perfect%' OR r.text LIKE '%good%' OR r.text LIKE '%personable%' OR r.text LIKE '%excellent%' OR r.text LIKE '%love%' OR r.text LIKE '%amazing%' OR r.text LIKE '%best%' OR r.text OR r.text LIKE '%affordable%' OR r.text LIKE '%pleased%' OR r.text LIKE '%pleasant%'LIKE '%favourite%' OR r.text LIKE '%great%'OR r.text LIKE '%well_done%' OR r.text LIKE '%delicious%'  THEN 'positive_review'
        WHEN r.text LIKE '%bad%' OR r.text LIKE '%hat%'  OR r.text LIKE '%skip%'OR r.text LIKE '%need%training%' OR r.text LIKE '%horrible%' OR r.text LIKE '%terrible%' OR r.text LIKE '%annoying%' OR r.text LIKE '%over%priced%' OR r.text LIKE '%wtf%' OR r.text LIKE '%rude%'OR r.text LIKE '%not%cool%'THEN 'Negative_review'
        ELSE 'Average_Review'
    END AS TypeofReview,
    r.text   
FROM
    business b
JOIN
    review r ON b.id = r.business_ID
WHERE b.stars BETWEEN 2 AND 3
ORDER BY B.city
LIMIT 5;
                          
iv. Output of your finished dataset:
                   
+----------------------+------------+-------+-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| name                 |  city      | stars | TypeofReview      | text                                                                                                                                                                              |
+----------------------+------------+-------+-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Dal Toro Ristorante  |  Las Vegas | 2.5   | positive_review   | We've made this our MUST STOP every time we stay in Vegas. The food blows our mind. Breakfast is always perfect & they pour the BEST cup of coffee in the world.!!!!              | 
| Mizuya               |  Las Vegas | 3.0   | positive_review   | We've eaten here several times.  The sushi is always good, as is the service.  Contrary to other reviews, I thought it was a nice calm quiet place to go.  Would eat here again!  |
| Markham Honda        |  Markham   | 2.3   | Negative_review   | I bring my car in here for servicing. I know car garages especially ones associated with dealershipa gets a bad rap. I've had bad  experiences here.                              |
| Elegant Car Rental   |  Brampton  | 1.5   | Negative_review   | Horrible service!! Will never go again!                                                                                                                                           |
| Cafe Tandoor         |  Aurora    | 3.5   | positive_review   | To make this place even more amazing, it is one of the places featured on WPXI's Just Pay Half Hot Card where you pay $25 for the card and it is worth $50 at local businesses.   |
+----------------------+------------+-------+-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

------------------------------------------------------------------------------
------------------------------------------------------------------------------

**Summary:**

Completing my Data Science certification SQL project was a hands-on journey that sharpened my skills in SQL and data analysis. From profiling the Yelp dataset to delving into Toronto's restaurant scene, I tackled various tasks, showcasing clarity in SQL code and analytical thinking.

In the final part, I opted for sentiment analysis, parsing Yelp reviews to categorize them as 'positive,' 'negative,' or 'average.' This project provided practical insights into data analysis, emphasizing its significance in the field of Data Science.
