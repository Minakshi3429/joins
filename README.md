# joins
#innner joins= types of joins ,where row is onlu included if its value is contained in both unique col of the table.
                An inner join is a join that outputs only rows that have an exact match in both tables being joined
Null values cant be used to link the rows ina join.
                #Our goal when we execute a JOIN or make a joined table is to use those common columns to let the database figure out which rows in one table match up to which rows in another table
                Q1 Dog owners who provided at least 10 ratings for one or more of their dogs in the ratings table. Of these owners, which 200 owners reported the highest average amount of surprise at their dog's performance, and what was the breed, breed_type, and breed_group of each of these owner's dog?
                ---to join a table we use a where clause and add a couple of details to the FROM clause so that the database knows from what table each field in your SELECT clause comes.
                %%%sql
SELECT d.dog_guid AS DogId , D.user_guid AS UserId, AVG(r.rating) AS AVGRating , COUNT(r.rating) AS NUMRating,d.breed , d.bree_type, d.breed_group
FROM dogs d , reviews r
WHERE d.dog_guid = r.dog_guid
GROUP BY DogId, UserId , AVGRating, NUMRating,d.breed,d.breed_type,d.breed_group
HAVING NUMRating >=10
ORDER BY AVGRating DESC
LIMIT 200 ;
----How would you extract the user_guid, dog_guid, breed, breed_type, and breed_group for all animals who completed the "Yawn Warm-up" game ?
%%sql
SELECT d.dog_guid AS DogID,d.user_guid AS UserID, d.breed, b.breed_type,b.breed_group
FROM dogs d , complete_tests c 
WHERE d.dog_guid=c.dog_guid AND test_name="Yawn Warm-up";
-----joing more than two tables (inner joins)
QQqq To extract the user_guid, user's state of residence, user's zip code, dog_guid, breed, breed_type, and breed_group for all animals who completed the "Yawn Warm-up" game, you might be tempted to query:
%%sql
SELECT d.user_guid AS UserID, u.state, u.zip, d.dog_guid AS DogID, d.breed, d.breed_type, d.breed_group
FROM dogs d, complete_tests c, users u
WHERE d.dog_guid=c.dog_guid 
   AND d.user_guid=u.user_guid
   AND c.test_name="Yawn Warm-up";
How would you extract the user_guid, membership_type, and dog_guid of all the golden retrievers who completed at least 1 Dognition test
SELECT DISTINCT d.user_guid AS UserID, u.membership_type, d.dog_guid AS DogID, d.breed 

FROM dogs d, complete_tests c, users u 

WHERE d.dog_guid=c.dog_guid 

AND d.user_guid=u.user_guid   

AND d.breed="golden retriever";
How many unique Golden Retrievers who live in North Carolina are there in the Dognition database ?

SELECT u.state AS state, d.breed AS breed, COUNT(DISTINCT d.dog_guid)

 
 FROM users u, dogs d 

WHERE d.user_guid=u.user_guid AND breed="Golden Retriever"

GROUP BY state 

HAVING state="NC";
   For which 3 dog breeds do we have the greatest amount of site_activity data,?
   SELECT d.breed, COUNT(s.script_detail_id) AS activity 

FROM dogs d, site_activities s 

WHERE d.dog_guid=s.dog_guid AND s.script_detail_id IS NOT NULL 

GROUP BY breed ORDER BY activity DESC


   
  
