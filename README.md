# DataLemurSQL

![alt text](https://datalemur.com/_next/image?url=%2Flogo.png&w=256&q=75 "DataLemur Logo")

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

`tweets` **Tweets**
| Column Name | Type    |
| ----------- | ------- |
| page_id     | integer |
| page_name   | varchar |

`tweets` **Tweets**
| page_id | Type                   |
| ------- | ---------------------- |
| 20001	  | SQL Solutions          |
| 20045	  | Brain Exercises        |
| 20701	  | Tips for Data Analysts |

`page_likes` **Example Input**
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
