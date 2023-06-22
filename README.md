# DataLemurSQL

![alt_text](https://datalemur.com/_next/image?url=%2Flogo.png&w=256&q=75 "DataLemur Logo")

Are you ready to crack the code to success in FAANG interviews? 🚀✨ 

In this post, I spill the beans on how I tackled DataLemur's challenging SQL questions - the same questions asked by top FAANG companies! 💼🔥 

Don't miss out on this golden opportunity to enhance your SQL prowess and impress recruiters. 💪📚🔓

Remember, practice makes perfect, and mastering SQL can be your key to unlocking career opportunities in the tech industry. 

Supercharge your skills and take the next big step in your professional journey. 

Click the link below and let the learning begin! 🎓💡

[Register Now and Ace Your FAANG SQL Interview Questions!](https://datalemur.com?referralCode=oW4bvkNc)

---

### Table of Contents
### EASY
1. [Page With No Likes [Facebook SQL Interview Question]](#easy1)
2. [Unfinished Parts [Tesla SQL Interview Question]](#easy2)
3. [Laptop vs. Mobile Viewership [New York Times SQL Interview Question]](#easy3)
4. [Data Science Skills [LinkedIn SQL Interview Question]](#easy4)
5. [Teams Power Users [Microsoft SQL Interview Question]](#easy5)

---

### <a id="easy1"></a>Page With No Likes (Easy) [Facebook SQL Interview Question]

Assume you're given the tables below about Facebook Page and Page likes (as in "Like a Facebook Page").

Write a query to return the IDs of the Facebook pages which do not possess any likes. The output should be sorted in ascending order.

`pages` **Table:**
| Column Name | Type    |
| ----------- | ------- |
| page_id     | integer |
| page_name   | varchar |

`pages` **Example Input:**
| page_id | Type                   |
| ------- | ---------------------- |
| 20001	  | SQL Solutions          |
| 20045	  | Brain Exercises        |
| 20701	  | Tips for Data Analysts |

`page_likes` **Table:**
| Column Name | Type     |
| ----------- | -------- |
| user_id     | integer  |
| page_id     | integer  |
| liked_date  | datetime |

`page_likes` **Example Input:**
| user_id |	page_id | liked_date          |
| ------- | ------- |-------------------- |
| 111	    | 20001	  | 04/08/2022 00:00:00 |
| 121	    | 20045	  | 03/12/2022 00:00:00 |
| 156	    | 20001	  | 07/25/2022 00:00:00 |

**Example Output**
| page_id |
| ------- |
| 20701   | 

**Solution**
<details>
  <summary>Click to reveal the solution</summary>
<pre><code>
WITH a AS
  (SELECT page_id
  FROM pages
  JOIN page_likes
  USING(page_id))
SELECT DISTINCT page_id
FROM pages
WHERE page_id NOT IN 
  (SELECT * FROM a)
ORDER BY 1;
</code></pre>
</details>

---

### <a id="easy2"></a>Unfinished Parts (Easy) [Tesla SQL Interview Question]

Tesla is investigating production bottlenecks and they need your help to extract the relevant data. Write a query that determines which parts with the assembly steps have initiated the assembly process but remain unfinished.

#### Assumptions:

##### ➼ parts_assembly table contains all parts currently in production, each at varying stages of the assembly process.

##### ➼ An unfinished part is one that lacks a `finish_date`.

This question is straightforward, so let's approach it with simplicity in both thinking and solution.

`parts_assembly` **Table:**
| Column Name   | Type     |
| ------------- | -------- |
| part          | string   |
| finish_date   | datetime |
| assembly_step | integer  |

`parts_assembly` **Example Input:**
| part    | finish_date         | assembly_step |
| ------- | ------------------- |-------------- |
| battery	| 01/22/2022 00:00:00	| 1             |
| battery	| 02/22/2022 00:00:00	| 2             |
| battery	| 03/22/2022 00:00:00	| 3             |
| bumper	| 01/22/2022 00:00:00	| 1             |
| bumper	| 02/22/2022 00:00:00	| 2             |
| bumper	|                     | 3             |
| bumper	| 		                | 4             |

**Example Output**
| part    | assembly_step |
| ------- |-------------- |
| bumper	| 3             |
| bumper	| 4             |

**Solution**
<details>
  <summary>Click to reveal the solution</summary>
<pre><code>
SELECT part, assembly_step
FROM parts_assembly
WHERE finish_date IS NULL
;
</code></pre>
</details>

---

### <a id="easy3"></a>Laptop vs. Mobile Viewership (Easy) [New York Times SQL Interview Question]

Assume you're given the table on user viewership categorised by device type where the three types are laptop, tablet, and phone.

Write a query that calculates the total viewership for laptops and mobile devices where mobile is defined as the sum of tablet and phone viewership. Output the total viewership for laptops as `laptop_reviews` and the total viewership for mobile devices as `mobile_views`.

`viewership` **Table:**
| Column Name |	Type                                 |
| ----------- | ------------------------------------ |
| user_id	    | integer                              |
| device_type	| string ('laptop', 'tablet', 'phone') |
| view_time	  | timestamp                            |

`viewership` **Example Input:**
| user_id |	device_type | view_time           |
| ------- | ----------- | ------------------- |
| 123	    | tablet	    | 01/02/2022 00:00:00 |
| 125	    | laptop	    | 01/07/2022 00:00:00 |
| 128     |	laptop	    | 02/09/2022 00:00:00 |
| 129     |	phone	      | 02/09/2022 00:00:00 |
| 145	    | tablet	    | 02/24/2022 00:00:00 |


**Example Output**
| laptop_views | mobile_views |
| ------------ | ------------ |
| 2          	 | 3            |

**Solution**
<details>
  <summary>Click to reveal the solution</summary>
<pre><code>
WITH a AS
  (SELECT COUNT(*) mobile_views
  FROM viewership
  WHERE device_type IN ('tablet', 'phone')),
b AS
  (SELECT COUNT(*) laptop_views
  FROM viewership
  WHERE device_type = 'laptop')
SELECT *
FROM b, a
;
</code></pre>
</details>

---

### <a id="easy4"></a>Data Science Skills (Easy) [LinkedIn SQL Interview Question]

Given a table of candidates and their skills, you're tasked with finding the candidates best suited for an open Data Science job. You want to find candidates who are proficient in Python, Tableau, and PostgreSQL.

Write a query to list the candidates who possess all of the required skills for the job. Sort the output by candidate ID in ascending order.

#### Assumption:

##### ➼ There are no duplicates in the candidates table.

`candidates` **Table:**
| Column Name  |	Type   |
| ------------ | ------- |
| candidate_id | integer |
| skill        | varchar |

`candidates` **Example Input:**
| candidate_id |	skill     |
| ------------ | ---------- | 
| 123	         | Python     |
| 123	         | Tableau    |
| 123	         | PostgreSQL |
| 234	         | R          |
| 234	         | PowerBI    |
| 234	         | SQL Server |
| 345	         | Python     |
| 345	         | Tableau    |

**Example Output**
| candidate_id | 
| ------------ | 
| 123       	 | 

**Solution**
<details>
  <summary>Click to reveal the solution</summary>
<pre><code>
SELECT candidate_id
FROM candidates
WHERE skill IN ('Python', 'Tableau', 'PostgreSQL')
GROUP BY candidate_id
HAVING COUNT(candidate_id) = 3
ORDER BY 1
;
</code></pre>
</details>

---

### <a id="easy5"></a>Teams Power Users (Easy) [Microsoft SQL Interview Question]

Write a query to identify the top 2 Power Users who sent the highest number of messages on Microsoft Teams in August 2022. Display the IDs of these 2 users along with the total number of messages they sent. Output the results in descending order based on the count of the messages.

##### Assumption:

##### ➼ No two users have sent the same number of messages in August 2022.

`messages` **Table:**
| Column Name |	Type     |
| ----------- | -------- |
| message_id  | integer  |
| sender_id   | integer  |
| receiver_id | integer  |
| content     | varchar  |
| sent_date   | datetime |

`messages` **Example Input:**
| message_id | sender_id | receiver_id | content                 | sent_date           |
| ---------- | --------- | ----------- | ----------------------- | ------------------- |
| 901        | 3601      | 4500        | You up?                 | 08/03/2022 00:00:00 | 
| 902        | 4500      | 3601        | Only if you're buying   | 08/03/2022 00:00:00 |
| 743	       | 3601      | 8752        | Let's take this offline | 06/14/2022 00:00:00 |
| 922        | 3601      | 4500        | Get on the call         | 08/10/2022 00:00:00 |

**Example Output**
| sender_id | message_count | 
| --------- | ------------- |
| 3601   	  | 2             |
| 4500      | 1             |

**Solution**
<details>
  <summary>Click to reveal the solution</summary>
<pre><code>
SELECT sender_id, COUNT(*) 
FROM messages
WHERE sent_date >= '08/01/22'
AND sent_date < '9/01/22'
GROUP BY sender_id
ORDER BY 2 DESC
LIMIT 2
;
</code></pre>
</details>

---
