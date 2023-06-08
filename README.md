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

### Page With No Likes (Easy) [Facebook SQL Interview Question]

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

### Unfinished Parts (Easy) [Tesla SQL Interview Question]

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

`page_likes` **Example Input:**
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
SELECT DISTINCT part 
FROM parts_assembly
WHERE finish_date IS NULL;
</code></pre>
</details>

---

### Laptop vs. Mobile Viewership (Easy) [New York Times SQL Interview Question]

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
