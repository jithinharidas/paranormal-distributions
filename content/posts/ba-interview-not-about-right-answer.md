---
title: "The Analyst Interview is Not About the Right Answer"
date: 2026-06-17
categories: ["Career"]
tags: ["interview", "analyst", "sql", "case study", "guesstimate"]
description: "The correct SQL query matters less than how you approached it. The right guesstimate number matters less than the structure you used to get there."
draft: false
---

Most people prepare for a analyst interview by practising answers.

That is the wrong thing to practise.

Interviewers are not checking your answer. They are watching how you got there. A wrong answer reached through good thinking is more impressive than a right answer that appeared from nowhere. A structured approach to a problem you cannot fully solve is more valuable than a perfect solution to the wrong question.

This post is about the three rounds most analyst interviews have, what interviewers are actually evaluating in each, and how to prepare for that instead of the answer.

---

## The SQL Round

The question is never really about SQL.

It looks like a SQL question. It has tables and columns and asks you to write a query. But what the interviewer is watching is whether you can translate a business question into a data question before you write a single line of code.

"Find the top 10 restaurants by order value last week, excluding cancelled orders."

Before you type anything, you should be asking: what counts as an order? Is last week Monday to Sunday or the last 7 days? What order statuses count as cancelled? These questions are not stalling. They are the job.

The SQL itself is secondary. Most interviewers do not care if you get the exact syntax right. They care if your logic is sound.

**What to actually study:**

**JOINs first.** INNER, LEFT, RIGHT. Know when to use each and why. Most interview questions involve at least two tables. Understanding which join preserves which rows is more important than anything else.

**Aggregations and GROUP BY.** SUM, COUNT, AVG, MAX, MIN. Know that WHERE filters before aggregation and HAVING filters after. This trips people up more than anything.

**Window functions.** This is where most candidates fall short and where you can stand out.

A window function does a calculation across a set of rows related to the current row, without collapsing the result into a single row the way GROUP BY does.

```sql
SELECT
  order_id,
  user_id,
  order_value,
  SUM(order_value) OVER (PARTITION BY user_id) AS total_user_spend,
  RANK() OVER (PARTITION BY city ORDER BY order_value DESC) AS rank_in_city,
  LAG(order_value) OVER (PARTITION BY user_id ORDER BY order_date) AS previous_order_value
FROM orders
```

The three most useful window functions to know:

**ROW_NUMBER / RANK / DENSE_RANK:** for ranking within a group. Use RANK when you want ties to share a rank. Use ROW_NUMBER when you need unique sequential numbers regardless of ties.

**LAG / LEAD:** for comparing a row to the previous or next row. Extremely useful for retention analysis, day-over-day comparisons, finding gaps between events.

**SUM / AVG / COUNT OVER:** for running totals or group-level metrics alongside row-level detail. Much cleaner than a subquery for many use cases.

Practice these until they feel natural. A candidate who reaches for a window function when it is the right tool immediately signals experience.

**CTEs** are also worth knowing. They make complex queries readable and are often the cleaner alternative to nested subqueries.

```sql
WITH active_users AS (
  SELECT user_id
  FROM orders
  WHERE order_date >= current_date - 30
  GROUP BY user_id
  HAVING COUNT(*) >= 2
)
SELECT COUNT(*) FROM active_users
```

---

## The Case Study Round

There is no right answer. The interviewer knows this going in.

What they are evaluating: do you clarify before you dive in, do you structure your thinking, do you consider both the user and the business, do you handle a pushback without falling apart.

The most common type of case study in analyst interviews at product companies is the metric movement question. Something dropped or something spiked and you have to figure out why.

**Example: DAU dropped 20% week over week. What do you do?**

Most candidates immediately start listing possible reasons. That is the wrong move. You do not have enough information yet.

Start with clarifying questions.

Is this a sudden drop or a gradual decline? Is it global or specific to a platform, region, or user segment? Did anything change recently: a release, a campaign, a competitor move. Is the data itself reliable, or could this be a tracking issue?

Then structure your investigation.

**Step 1: Validate the data.** Is this real or is a pipeline broken? Check if other metrics moved in a correlated way. If DAU dropped but sessions did not, something is wrong with the measurement.

**Step 2: Segment the drop.** Where is it coming from? New users or returning users? iOS or Android? A specific city? A specific feature? A 20% overall drop that is entirely explained by one city on one platform is a very different problem from a broad decline across all segments.

**Step 3: Check for external causes.** Public holiday, competitor promotion, news event, payment gateway outage. These happen more often than people think.

**Step 4: Check internal causes.** Recent app update, push notification change, pricing change, feature removal.

**Step 5: Propose next steps.** Based on what you find, what do you investigate further and how?

The interviewer will push back somewhere in this process. That is intentional. They want to see if you defend your thinking or fold immediately. You can update your position if the pushback makes sense. You should not abandon your structure just because someone challenged it.

---

## The Guesstimate Round

The number does not matter.

Read that again, because it is the thing most people do not believe until they have done a few interviews.

Nobody knows how many pizzas are sold in Bengaluru in a day. The interviewer does not know. You do not know. Nobody in the room knows. What the interviewer wants to see is whether you can build a reasonable structure to approach a problem where you do not have the answer.

**Example: How many pizzas are sold in Bengaluru per day?**

Before you start calculating, do two things. Clarify the scope: are we talking delivery only or all consumption including restaurants and quick service counters? And state that you are going to approach this from two sides and then see if the answers are in the same ballpark.

There are two ways to approach a guesstimate. Come at it from the demand side or the supply side. Doing both and checking whether they roughly agree is one of the best signals you can send in an interview.

**Demand side approach:**

Start with the population and work down to the behaviour.

Bengaluru population: roughly 13 million people.
Average household size: 3 to 4 people. So around 3.5 million households.

Now segment those households. Not everyone eats pizza with the same frequency.

Higher income households, maybe 20% of the total, probably order pizza once or twice a week. That is around 700,000 households ordering maybe 1.5 times a week on average, so about 150,000 pizza orders from this segment per week, or 21,000 per day.

Middle income households, maybe 50% of the total, order pizza a few times a month. Say twice a month. That is 1.75 million households, 2 orders per month, so 3.5 million orders per month from this segment, or around 117,000 per day.

Lower income households, the remaining 30%, rarely order pizza. Maybe once every two to three months. 1.05 million households, roughly 0.4 orders per month per household, gives about 420,000 orders per month or 14,000 per day.

Total online delivery estimate: roughly 150,000 pizzas per day.

But delivery is only part of the picture. People also eat pizza at restaurants, at office cafeterias, and from quick service counters at malls. Offline consumption might be another 40 to 50 percent on top of delivery.

Total demand side estimate: 210,000 to 225,000 pizzas per day.

**Supply side approach:**

Now come at it from the other direction and see if it holds up.

How many pizza outlets are there in Bengaluru? Food delivery platforms list somewhere around 2,000 to 3,000 pizza options across all formats but not all of these are dedicated pizza outlets. Some are cloud kitchens sharing a listing, some are multi-cuisine places that happen to list pizza. Estimate around 800 to 1,000 dedicated pizza outlets of varying sizes.

Break them down by type:

Large chain outlets like Domino's and Pizza Hut. Bengaluru has around 150 to 200 of these. A busy outlet might sell 200 to 300 pizzas on a weekday and more on weekends. Average across the week: 200 per day. That gives roughly 35,000 to 40,000 pizzas per day just from large chains.

Mid-size standalone pizza restaurants. Maybe 300 to 400 across the city. These sell fewer. Average 60 to 80 pizzas per day. That is 20,000 to 30,000 pizzas per day.

Small places, cloud kitchens, bakeries with pizza on the menu. Perhaps 500 to 600 of these. Much lower volume, maybe 20 to 30 per day each. That is 10,000 to 18,000 pizzas per day.

Total supply side estimate: 65,000 to 88,000 pizzas per day from dedicated outlets. Add informal supply not captured here, maybe another 30 percent, and you get 85,000 to 115,000 pizzas per day.

**Reconciling the two approaches:**

The demand side gives you 210,000 to 225,000. The supply side gives you 85,000 to 115,000. They are not in the same ballpark, which means one of your assumptions is off.

This is actually fine. This is what a good guesstimate looks like. You found a discrepancy and now you think through why.

Possible reasons: the demand side might be overestimating frequency in middle income households. The supply side might be underestimating the number of outlets or missing a large segment. Probably both are a little off.

You might settle on 150,000 to 175,000 as your final estimate, explain your reasoning for landing there between the two approaches, and flag the assumptions you are least confident about.

The interviewer is watching all of this. They are not checking your arithmetic. They are checking whether you can navigate uncertainty, whether you segment intelligently, whether you think about online and offline separately, whether you catch your own inconsistencies, and whether you can explain your thinking clearly while doing it.

**One more thing worth saying out loud:**

State every assumption as you make it. Do not use a number silently. Say "I am assuming Bengaluru has around 13 million people" and "I am assuming a middle income household orders pizza about twice a month." This serves two purposes. It shows your reasoning. And it gives the interviewer a chance to correct you if you are wildly off, which is actually helpful.

**A note on practice:**

This walkthrough is more detailed than what you would say in an actual interview, which typically runs 10 to 15 minutes for a guesstimate. The point is to show you all the components: segmentation, two-sided approach, reconciliation, assumption flagging.

In practice, you would move faster and skip some of the granularity. But you need to understand each piece before you can condense it. Practice guesstimates out loud, with a timer, with someone who will push back on your assumptions. The structure becomes natural only through repetition.

Good questions to practice on:
- How many cups of chai are consumed in India per day?
- How many Uber rides happen in Mumbai on a weekday?
- How many wedding photographers are there in India?
- How many gym memberships are active in Bengaluru?

Each of these has a demand side and a supply side. Each has online and offline components. Each requires you to segment the population meaningfully before you start multiplying numbers.

The goal is not to get the right answer. The goal is to build the habit of structured thinking under pressure. Do that consistently and the number will take care of itself.

---

## The thing that connects all three

SQL, case study, guesstimate. Three different formats, same underlying evaluation.

Can you structure a problem before you solve it? Can you communicate your thinking as you go? Can you handle uncertainty without panicking? Can you update your position when new information arrives without losing the thread of your argument?

These are not interview skills. These are the actual skills of the job.

The interview is not testing whether you know the right answer. It is testing whether you are the kind of person who finds the right answer. Those are very different things, and the preparation for each is very different.

Practise thinking out loud. Practise asking clarifying questions before you start. Practise being wrong partway through and correcting yourself without losing confidence.

The answer matters less than you think. The approach is the whole thing.
