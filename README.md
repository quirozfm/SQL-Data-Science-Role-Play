Data Scientist Role Play: Profiling and Analyzing the Yelp Dataset Coursera Worksheet

This is a 2-part assignment. In the first part, you are asked a series of questions that will help you profile and understand the data just like a data scientist would. For this first part of the assignment, you will be assessed both on the correctness of your findings, as well as the code you used to arrive at your answer. You will be graded on how easy your code is to read, so remember to use proper formatting and comments where necessary.

In the second part of the assignment, you are asked to come up with your own inferences and analysis of the data for a particular research question you want to answer. You will be required to prepare the dataset for the analysis you choose to do. As with the first part, you will be graded, in part, on how easy your code is to read, so use proper formatting and comments to illustrate and communicate your intent as required.

For both parts of this assignment, use this "worksheet." It provides all the questions you are being asked, and your job will be to transfer your answers and SQL coding where indicated into this worksheet so that your peers can review your work. You should be able to use any Text Editor (Windows Notepad, Apple TextEdit, Notepad ++, Sublime Text, etc.) to copy and paste your answers. If you are going to use Word or some other page layout application, just be careful to make sure your answers and code are lined appropriately.
In this case, you may want to save as a PDF to ensure your formatting remains intact for you reviewer.



Part 1: Yelp Dataset Profiling and Understanding

1. Profile the data by finding the total number of records for each of the tables below:
	
i. Attribute table =10000
ii. Business table = 10000
iii. Category table = 10000
iv. Checkin table = 10000
v. elite_years table =10000
vi. friend table = 10000
vii. hours table =10000
viii. photo table = 10000
ix. review table = 10000
x. tip table = 10000
xi. user table =10000
	


2. Find the total distinct records by either the foreign key or primary key for each table. If two foreign keys are listed in the table, please specify which foreign key.

    i.   Business    =  id             			10000
	ii.  Hours       =  business_id    			1562
	iii. Category    =  business_id    			2643
	iv.  Attribute   =  business_id	 			1115
	v.   Review      =	id,business_id,user_id	10000,8090,9581
	vi.  Checkin     = 	business_id				493
	vii. Photo       =	id,business_id			10000, 6493
	viii.Tip         = 	business_id ,user_id	3979,537
	ix.  User        = 	id						10000
	x.   Friend      = 	user_id					11
	xi.  Elite_years =	user_id 				2780

Note: Primary Keys are denoted in the ER-Diagram with a yellow key icon.	
  
  SELECT COUNT ( DISTINCT (Key) )from table ( General format)

  SELECT COUNT (distinct id ) from business
	  SELECT COUNT (distinct business_id ) from hours
	  SELECT COUNT (distinct business_id ) from Category
	  SELECT COUNT (distinct business_id ) from Attribute
	  SELECT COUNT (distinct id), count(distinct business_id), 
	  SELECT COUNT(distinct user_id) from review
	  SELECT COUNT (distinct business_id ) from Checkin
	  SELECT COUNT (distinct id ), count(distinct business_id ) from photo
	  SELECT COUNT (distinct business_id ),count ( distinct user_id) from tip
	  SELECT COUNT (distinct id ) from User
	  SELECT COUNT (distinct user_id ) from Friend
	  SELECT COUNT (distinct user_id ) from Elite_yers	  


3. Are there any columns with null values in the Users table? Indicate "yes," or "no."

	Answer: NO
	
	
	SQL code used to arrive at answer:
	
	SELECT COUNT(* ) from User
		where id is NULL OR
			  name is NULL OR
			  review_count IS NULL OR
			  yelping_since IS NULL OR
			  useful IS NULL OR 
			  funny IS NULL OR 
			  cool IS NULL OR 
			  fans IS NULL OR 
			  average_stars IS NULL OR 
			  compliment_hot IS NULL OR 
			  compliment_more IS NULL OR 
			  compliment_profile IS NULL OR 
			  compliment_cute IS NULL OR 
			  compliment_list IS NULL OR 
			  compliment_note IS NULL OR 
			  compliment_plain IS NULL OR 
			  compliment_cool IS NULL OR 
			  compliment_funny IS NULL OR 
			  compliment_writer IS NULL OR 
			  compliment_photos IS NULL

	
4. For each table and column listed below, display the smallest (minimum), largest (maximum), and average (mean) value for the following fields:

	i. Table: Review, Column: Stars

	SELECT min(stars),max(stars), avg(stars) from Review

		min:		max:		avg:
		 1			 5			3.7082
		
	
	ii. Table: Business, Column: Stars
	
	SELECT min(stars),max(stars), avg(stars) from Business

		min:		max:		avg:
		 1			 53			1.9414
		
	
	iii. Table: Tip, Column: Likes
	
	SELECT min(likes),max(likes), avg(likes) from Tip
	
		 0			 2          0.0144

		
	
	iv. Table: Checkin, Column: Count
	
	SELECT min(count),max(count), avg(count) from Checkin

		min:		max:		avg:
		 1			 53			1.9414
	
	v. Table: User, Column: Review_count

	SELECT min(Review_count),max(Review_count), avg(Review_count) from User
	
		 0			2000		24.2995
		


5. List the cities with the most reviews in descending order:

	SQL code used to arrive at answer:
	
	SELECT city,sum(review_count) as reviews 
		FROM business
		Group By city
		Order By reviews desc	

	Copy and Paste the Result Below:
+-----------------+---------+
| city            | reviews |
+-----------------+---------+
| Las Vegas       |   82854 |
| Phoenix         |   34503 |
| Toronto         |   24113 |
| Scottsdale      |   20614 |
| Charlotte       |   12523 |
| Henderson       |   10871 |
| Tempe           |   10504 |
| Pittsburgh      |    9798 |
| Montréal        |    9448 |
| Chandler        |    8112 |
| Mesa            |    6875 |
| Gilbert         |    6380 |
| Cleveland       |    5593 |
| Madison         |    5265 |
| Glendale        |    4406 |
| Mississauga     |    3814 |
| Edinburgh       |    2792 |
| Peoria          |    2624 |
| North Las Vegas |    2438 |
| Markham         |    2352 |
| Champaign       |    2029 |
| Stuttgart       |    1849 |
| Surprise        |    1520 |
| Lakewood        |    1465 |
| Goodyear        |    1155 |
+-----------------+---------+
(Output limit exceeded, 25 of 362 total rows shown)
	
6. Find the distribution of star ratings to the business in the following cities:

i. Avon

SQL code used to arrive at answer:

		SELECT stars, sum(review_count) from business
		Where city = 'Avon'
		Group By stars

Copy and Paste the Resulting Table Below (2 columns – star rating and count):
+-------+-------------------+
| stars | sum(review_count) |
+-------+-------------------+
|   1.5 |                10 |
|   2.5 |                 6 |
|   3.5 |                88 |
|   4.0 |                21 |
|   4.5 |                31 |
|   5.0 |                 3 |
+-------+-------------------+

ii. Beachwood

SQL code used to arrive at answer:

		SELECT stars, sum(review_count) from business
		WHERE city = 'Beachwood'
		Group By stars
		
Copy and Paste the Resulting Table Below (2 columns – star rating and count):
		
		+-------+-------------------+
		| stars | sum(review_count) |
		+-------+-------------------+
		|   2.0 |                 8 |
		|   2.5 |                 3 |
		|   3.0 |                11 |
		|   3.5 |                 6 |
		|   4.0 |                69 |
		|   4.5 |                17 |
		|   5.0 |                23 |
		+-------+-------------------+	

7. Find the top 3 users based on their total number of reviews:
		
	SQL code used to arrive at answer:

	SELECT id, name , review_count from user
		Order By review_count desc
		Limit 3
		
	Copy and Paste the Result Below:
		
		+------------------------+--------+--------------+
		| id                     | name   | review_count |
		+------------------------+--------+--------------+
		| -G7Zkl1wIWBBmD0KRy_sCw | Gerald |         2000 |
		| -3s52C4zL_DHRK0ULG6qtg | Sara   |         1629 |
		| -8lbUNlXVSoXqaRRiHiSNg | Yuri   |         1339 |
		+------------------------+--------+--------------+	

8. Does posing more reviews correlate with more fans?

	Please explain your findings and interpretation of the results:
	
	No, posing more reviews do not correlate with more fans. Take a look at fans vs reveiws.

			   select id,
		       name,
		       review_count,
		       fans,
		       yelping_since
		FROM user
		ORDER BY fans desc
		
		+------------------------+-----------+--------------+------+---------------------+
		| id                     | name      | review_count | fans | yelping_since       |
		+------------------------+-----------+--------------+------+---------------------+
		| -9I98YbNQnLdAmcYfb324Q | Amy       |          609 |  503 | 2007-07-19 00:00:00 |
		| -8EnCioUmDygAbsYZmTeRQ | Mimi      |          968 |  497 | 2011-03-30 00:00:00 |
		| --2vR0DIsmQ6WfcSzKWigw | Harald    |         1153 |  311 | 2012-11-27 00:00:00 |
		| -G7Zkl1wIWBBmD0KRy_sCw | Gerald    |         2000 |  253 | 2012-12-16 00:00:00 |
		| -0IiMAZI2SsQ7VmyzJjokQ | Christine |          930 |  173 | 2009-07-08 00:00:00 |
		| -g3XIcCb2b-BD0QBCcq2Sw | Lisa      |          813 |  159 | 2009-10-05 00:00:00 |
		| -9bbDysuiWeo2VShFJJtcw | Cat       |          377 |  133 | 2009-02-05 00:00:00 |
		| -FZBTkAZEXoP7CYvRV2ZwQ | William   |         1215 |  126 | 2015-02-19 00:00:00 |
		| -9da1xk7zgnnfO1uTVYGkA | Fran      |          862 |  124 | 2012-04-05 00:00:00 |
		| -lh59ko3dxChBSZ9U7LfUw | Lissa     |          834 |  120 | 2007-08-14 00:00:00 |
		| -B-QEUESGWHPE_889WJaeg | Mark      |          861 |  115 | 2009-05-31 00:00:00 |
		| -DmqnhW4Omr3YhmnigaqHg | Tiffany   |          408 |  111 | 2008-10-28 00:00:00 |
		| -cv9PPT7IHux7XUc9dOpkg | bernice   |          255 |  105 | 2007-08-29 00:00:00 |
		| -DFCC64NXgqrxlO8aLU5rg | Roanna    |         1039 |  104 | 2006-03-28 00:00:00 |
		| -IgKkE8JvYNWeGu8ze4P8Q | Angela    |          694 |  101 | 2010-10-01 00:00:00 |
		| -K2Tcgh2EKX6e6HqqIrBIQ | .Hon      |         1246 |  101 | 2006-07-19 00:00:00 |
		| -4viTt9UC44lWCFJwleMNQ | Ben       |          307 |   96 | 2007-03-10 00:00:00 |
		| -3i9bhfvrM3F1wsC9XIB8g | Linda     |          584 |   89 | 2005-08-07 00:00:00 |
		| -kLVfaJytOJY2-QdQoCcNQ | Christina |          842 |   85 | 2012-10-08 00:00:00 |
		| -ePh4Prox7ZXnEBNGKyUEA | Jessica   |          220 |   84 | 2009-01-12 00:00:00 |
		| -4BEUkLvHQntN6qPfKJP2w | Greg      |          408 |   81 | 2008-02-16 00:00:00 |
		| -C-l8EHSLXtZZVfUAUhsPA | Nieves    |          178 |   80 | 2013-07-08 00:00:00 |
		| -dw8f7FLaUmWR7bfJ_Yf0w | Sui       |          754 |   78 | 2009-09-07 00:00:00 |
		| -8lbUNlXVSoXqaRRiHiSNg | Yuri      |         1339 |   76 | 2008-01-03 00:00:00 |
		| -0zEEaDFIjABtPQni0XlHA | Nicole    |          161 |   73 | 2009-04-30 00:00:00 |
		+------------------------+-----------+--------------+------+---------------------+
	
9. Are there more reviews with the word "love" or with the word "hate" in them?

	Answer:There are more reviews with the word "Love" than "Hate"


	
	SQL code used to arrive at answer:

	SELECT 	count(*) as hatecount from review			SELECT 	count(*) as lovecount from review
		Where text LIKE "%hate%"                            		Where text LIKE "%love%"
		+-----------+							  +-----------+
		| hatecount |							  | lovecount |
		+-----------+							  +-----------+
		|       232 |							  |      1780 |
		+-----------+							  +-----------+
	
10. Find the top 10 users with the most fans:

	SQL code used to arrive at answer:
	
	SELECT id, name ,fans
		FROM user 
		Order By fans desc
		Limit 10
	
	Copy and Paste the Result Below:

	+------------------------+-----------+------+
		| id                     | name      | fans |
		+------------------------+-----------+------+
		| -9I98YbNQnLdAmcYfb324Q | Amy       |  503 |
		| -8EnCioUmDygAbsYZmTeRQ | Mimi      |  497 |
		| --2vR0DIsmQ6WfcSzKWigw | Harald    |  311 |
		| -G7Zkl1wIWBBmD0KRy_sCw | Gerald    |  253 |
		| -0IiMAZI2SsQ7VmyzJjokQ | Christine |  173 |
		| -g3XIcCb2b-BD0QBCcq2Sw | Lisa      |  159 |
		| -9bbDysuiWeo2VShFJJtcw | Cat       |  133 |
		| -FZBTkAZEXoP7CYvRV2ZwQ | William   |  126 |
		| -9da1xk7zgnnfO1uTVYGkA | Fran      |  124 |
		| -lh59ko3dxChBSZ9U7LfUw | Lissa     |  120 |
		+------------------------+-----------+------+
		

Part 2: Inferences and Analysis

1. Pick one city and category of your choice and group the businesses in that city or category by their overall star rating. Compare the businesses with 2-3 stars to the businesses with 4-5 stars and answer the following questions. Include your code.
	
i. Do the two groups you chose to analyze have a different distribution of hours?

Yes ,they do have different distribution hours. For example for the restaurant category in the Phoenix city , the one with 2-3 star
ratings operates for longer hoursthan the one with 4-5 star ratings.


ii. Do the two groups you chose to analyze have a different number of reviews?
         
Yes they have different number of reviews.

iii. Are you able to infer anything from the location data provided between these two groups? Explain.

No, I wasn't able to infer anything since two groups had different zipcodes

SQL code used for analysis:

SELECT B.name ,
              	       C.category,
		       B.city, 
		       B.postal_code as zipcode
		       hours , 
		       CASE
			   WHEN stars BETWEEN 2 AND 3 THEN '2-3 stars'
			   WHEN stars BETWEEN 4 AND 5 THEN '4-5 stars'
		      END AS rating,
		      B.review_count as reviews
       		From business B
		Inner join hours H  on B.id = H.business_id
		Inner join category C on C.business_id = B.id
		Where city = 'Phoenix' and category = 'Restaurants' and rating in ('2-3 stars','4-5 stars')
		Group By name
		Order By stars desc		
		
2. Group business based on the ones that are open and the ones that are closed. What differences can you find between the ones that are still open and the ones that are closed? List at least two differences and the SQL code you used to arrive at your answer.
		
i. Difference 1:
         
The average review count was 9 points more for business that are open  than the business that are closed
             
ii. Difference 2:
         
The number of distinct business_id for the one that are open is 5 times more than the business that are closed and hence the 
average review count is higher for the business that are open
                
         
SQL code used for analysis:

SELECT count(distinct id), 
			   count(distinct city),
			   avg(stars), 
               		   avg(review_count),
			   is_open
		From business
		Broup By is_open	
	
3. For this last part of your analysis, you are going to choose the type of analysis you want to conduct on the Yelp dataset and are going to prepare the data for analysis.

Ideas for analysis include: Parsing out keywords and business attributes for sentiment analysis, clustering businesses to find commonalities or anomalies between them, predicting the overall star rating for a business, predicting the number of fans a user will have, and so on. These are just a few examples to get you started, so feel free to be creative and come up with your own problem you want to solve. Provide answers, in-line, to all of the following:
	
i. Indicate the type of analysis you chose to do:
         
I chose to analyse whether the businesses like restaurants having the arrtibutes like 'goodforkids' ,'alcohol' and 'free wifi'  
	   relate to the number of stars or the review counts that they get. I chose particulrly  the state 'Arizona'  as this state  has more 
	   number of restaurants, has the review counts ranging from  the least to the highest and the ratings from 2 to 4.5 stars, more restaurants increase possibility for effective analysis. 

ii. Write 1-2 brief paragraphs on the type of data you will need for your analysis and why you chose that data:
                           
    I used 3 tables like business, category and attribute for my analysis. 
	I chose the business name ,their catagory , the state in which they are run , the attributes they have, their ratings and their count of
	reviews. I took varibles like  
	
	1)name, state, stars , review_count from  the table business, 
	2)category from the table category and
	3)name ,value from the attribute table.
	
	To connect all the 3 tables. I used the primary keys like id from business, business_id from category and 
	business_id from attribute table.
                 
	I wanted to know having a free wifi or restaurents good for kids or having full-bar or having any combination of 2 or all the attributes 
	contributes to good rating or having more reviews in particular.       

iii. Output of your finished dataset:

   +----------------------------------------+-------------+---------------+-------+-------+--------------+
		| name                                   | name        | value         | state | stars | review_count |
		+----------------------------------------+-------------+---------------+-------+-------+--------------+
		| Charlie D's Catfish & Chicken          | Alcohol     | none          | AZ    |   4.5 |            7 |
		| Charlie D's Catfish & Chicken          | WiFi        | no            | AZ    |   4.5 |            7 |
		| Charlie D's Catfish & Chicken          | GoodForKids | 1             | AZ    |   4.5 |            7 |
		| Bootleggers Modern American Smokehouse | Alcohol     | full_bar      | AZ    |   4.0 |          431 |
		| Bootleggers Modern American Smokehouse | WiFi        | no            | AZ    |   4.0 |          431 |
		| Bootleggers Modern American Smokehouse | GoodForKids | 1             | AZ    |   4.0 |          431 |
		| The Cider Mill                         | Alcohol     | full_bar      | AZ    |   4.0 |           91 |
		| The Cider Mill                         | WiFi        | no            | AZ    |   4.0 |           91 |
		| The Cider Mill                         | GoodForKids | 1             | AZ    |   4.0 |           91 |
		| Nabers Music, Bar & Eats               | Alcohol     | full_bar      | AZ    |   4.0 |           75 |
		| Senor Taco                             | Alcohol     | none          | AZ    |   3.5 |           83 |
		| Senor Taco                             | WiFi        | no            | AZ    |   3.5 |           83 |
		| Senor Taco                             | GoodForKids | 1             | AZ    |   3.5 |           83 |
		| Five Guys                              | Alcohol     | none          | AZ    |   3.5 |           63 |
		| Five Guys                              | WiFi        | no            | AZ    |   3.5 |           63 |
		| Five Guys                              | GoodForKids | 1             | AZ    |   3.5 |           63 |
		| Gallagher's                            | Alcohol     | full_bar      | AZ    |   3.0 |           60 |
		| Gallagher's                            | WiFi        | free          | AZ    |   3.0 |           60 |
		| Gallagher's                            | GoodForKids | 1             | AZ    |   3.0 |           60 |
		| Mango Flats                            | Alcohol     | beer_and_wine | AZ    |   2.5 |            5 |
		| Mango Flats                            | WiFi        | free          | AZ    |   2.5 |            5 |
		| Mango Flats                            | GoodForKids | 1             | AZ    |   2.5 |            5 |
		| Famous Sam's                           | Alcohol     | full_bar      | AZ    |   2.5 |            3 |
		| Famous Sam's                           | GoodForKids | 0             | AZ    |   2.5 |            3 |
		| McDonald's                             | Alcohol     | none          | AZ    |   2.0 |            8 |
		| McDonald's                             | WiFi        | free          | AZ    |   2.0 |            8 |
		| McDonald's                             | GoodForKids | 1             | AZ    |   2.0 |            8 |
		+----------------------------------------+-------------+---------------+-------+-------+--------------+
		      
         
iv. Provide the SQL code you used to create your final dataset:

select b.name as business, 
					a.name as attribute,
					a.value,
					b.state, 
					b.stars,
					b.review_count
			from business b
			inner join category c on c.business_id = b.id
			inner join attribute a on a.business_id = b.id
			where (a.name like  'alcohol' or 
					a.name like 'wifi' or 
					a.name like 'goodforkids') and 
					category = 'Restaurants' and b.state ='AZ'
			order by  stars desc ,
						review_count 

