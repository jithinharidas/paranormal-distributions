---
title: "The Model Said 0.91. My Stakeholder Said Prove It."
date: 2026-05-03
categories: ["Analytics"]
tags: ["rfm", "machine learning", "stakeholders", "communication", "lifetime value"]
description: "AUC is for you. Revenue per cohort is for them. Both are true. Only one lands in a meeting."
draft: false
---

You built the model. You checked the AUC. 0.91. You have read the [previous post](/posts/teaching-a-machine-who-your-best-customers-are/) so you know that is a good number. You walk into the room feeling good about yourself.

The first question is: "what does 0.91 mean?"

You explain it. The one who churned vs the one who did not, the model ranks them correctly 91% of the time. You can see from the face across the table that this has not landed. Not because they are not smart. Because 0.91 is your number, not theirs. You are speaking a language they did not ask to learn.

This is the part of analytics nobody writes about. Getting the model right is one problem. Getting someone to believe in it is a completely different one.

---

## What actually worked

I did not win the argument by explaining AUC better.

I won it by showing something the stakeholder already understood: the difference in lifetime value between cohorts.

Champions spend significantly more than At Risk users over their lifetime. At Risk users spend more than Dormants. Dormants are basically ghosts in your revenue numbers. This is not a model output. This is just the data, described simply. No probability scores. No curves. Just: these users are worth this much, those users are worth that much, and here is the gap between them.

{{< diagram-ltv >}}

The room changes when you show this. Because now the segmentation is not an abstract statistical exercise. It is a revenue conversation. And everyone in that room speaks revenue.

The model becomes credible not because you defended the methodology. It becomes credible because the business reality it is pointing at is undeniable.

---

## The translation problem

Here is something worth writing down somewhere.

Every metric you care about as an analyst has a translation. AUC does not mean anything to a stakeholder. What it means is: if you gave the model a list of 1,000 users and asked it to rank them by churn risk, the actual churners would cluster near the top. That is it. That is the whole thing.

Feature importance does not mean anything to a stakeholder. What it means is: the three things that matter most for predicting whether someone will churn are how recently they ordered, how often they ordered before that, and how long they have been a customer.

{{< diagram-translation >}}

Your job in the meeting is not to defend the model. Your job is to translate it into something that connects to a decision someone in that room actually has to make.

If you cannot do that, the model does not matter how good it is.

---

## The question that actually matters

After the LTV chart landed, the next question was better. Not "what does 0.91 mean" but "so which of these groups should we focus the campaign on?"

That is the question you want. Because now you are talking about action, not methodology.

At Risk users are the answer, almost always. They have demonstrated enough value to be worth the effort. They have not been gone long enough to be unrecoverable. They are close enough to the edge that a well-timed nudge might actually work. Champions do not need the campaign. They are already yours. Dormants probably will not respond regardless of what you send.

The model helps you rank within the At Risk group, from most likely to churn to least. You do not have to reach all 200,000 of them. You reach the top 10% and see what happens.

---

## The meeting that goes sideways anyway

None of this guarantees a clean outcome.

Someone will ask if you can do this in Excel. Someone will say the sample size feels small. Someone will bring up a campaign from two years ago that targeted a similar cohort and did not work. Someone will ask whether the model accounts for seasonality.

Some of these are good questions. Some of them are not questions at all, just discomfort with something new wearing the costume of a question.

The best thing you can do is not get defensive. Answer what you can. Acknowledge what you cannot. Offer to follow up on the things that need more thought.

The model does not win the room. You do. The model just gives you something real to stand behind.

---

## What I actually took away from this

Stakeholders are not the obstacle. The translation is the obstacle.

0.91 is a precise, meaningful number that tells you something true about how the model performs. It is also completely useless in a business meeting unless you can connect it to something the person across the table is already thinking about.

The LTV chart did that. It showed the business reality that the model was built to serve. Once the reality landed, the model became a tool rather than a claim that needed defending.

That is the version of this conversation that goes well. You stop trying to explain the AUC and start showing what happens when you act on it.

The model said 0.91. The stakeholder eventually said fine. It just took a chart about revenue to get there.
