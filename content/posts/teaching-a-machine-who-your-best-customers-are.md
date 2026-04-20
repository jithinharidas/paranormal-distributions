---
title: "Teaching a Machine Who Your Best Customers Are"
date: 2026-04-26
categories: ["Analytics"]
tags: ["rfm", "machine learning", "classification", "roc-auc", "retention"]
description: "RFM segments tell you where your users are. A prediction model tells you where they are going. Here is how to build one and how to know if it actually works."
draft: false
---

The [previous post](/posts/not-all-users-are-your-users/) left you with six user archetypes and a ranked list of segments. Champions, Loyals, At Risk, One-Order Wonders, Dormants, and the occasional unpredictable person who replies to a three-day-old message like it just came in.

You know who is who. Now what?

Here is the problem nobody mentions. Your At Risk segment has 200,000 users. You cannot re-engage all of them. Budget does not exist for that. Neither does the time. And honestly, not all of them are worth the same effort. Some of them are four days away from ordering again anyway. Some of them checked out fourteen months ago and are not coming back under any circumstances.

The segment tells you the neighbourhood. What you actually need is the specific address.

This is where a prediction model comes in. And this post is about building one, understanding what makes it good, and knowing when it is lying to you.

---

## The question you are actually asking

A prediction model answers one yes or no question about a user.

Will this person order again in the next 30 days?

Not "what segment are they in." Not "what is their lifetime value." Just: will they come back or not? Yes or no.

The model does not spit out yes or no directly. It gives you a probability. Something like 0.82, meaning there is an 82% chance this user will order again. You then draw a line somewhere, say 0.5, and everyone above it gets classified as "will order," everyone below as "will not."

You can move that line up or down depending on what you are trying to do. More on why that matters shortly.

The model learns from history. You give it data about 100,000 users from six months ago, tell it which ones ordered in the following 30 days and which ones did not, and ask it to find the pattern. That is supervised learning. You are giving it the answers to past questions so it can answer future ones.

---

## What you feed it

For an RFM-based model, most of the inputs are things you already have.

Days since last order. Total number of orders. Average order value. Whether the gap between orders is getting longer or shorter. How long the user has been a customer.

A newer user with low frequency is normal. An older user with low frequency is a signal. The model learns to tell the difference.

You can add more — what channel the user came from, what time of day they usually order, whether they used a discount on their last order. The general principle is to give the model everything you know that might be relevant, and let it figure out which things actually matter. It is surprisingly good at this.

---

## Why accuracy will get you into trouble

Here is the part that trips most people up.

Suppose 90% of the users in your dataset did not order in the 30-day window you are predicting. A model that predicts "will not order" for every single user, without looking at any features at all, would be 90% accurate.

That model is completely useless. You would never identify a single person worth reaching out to. But by the accuracy metric, it looks like a strong result.

This is called the class imbalance problem. When one outcome is much more common than the other, accuracy is a terrible way to measure whether your model is actually working.

Think of it like a weather app that always predicts "sunny" in Bangalore from February to May. Technically right most of the time. Absolutely useless the one week it actually matters.

{{< diagram-confusion >}}

What you want to know is something more specific: when the model says someone is going to churn, are they actually churning? And when someone actually churns, is the model catching them? These are two different questions and they have names.

**Precision** is the first one. Of everyone the model flagged as high churn risk, what fraction actually churned?

**Recall** is the second. Of everyone who actually churned, what fraction did the model catch?

These two numbers are in tension. Lower the threshold and you catch more churners but also flag a lot of people who were fine. Recall goes up, precision goes down. Raise it and you are more selective but you miss people. The threshold is a business decision, not a model decision.

---

## The one number that actually tells you if your model is good

The ROC-AUC. Receiver Operating Characteristic, Area Under the Curve. A name that explains absolutely nothing about what it does, which is very on-brand for statistics.

Here is what it actually measures.

Imagine you pick two users at random. One who churned, one who did not. The AUC is the probability that your model correctly assigns the higher churn probability to the one who actually churned.

AUC of 0.5: the model is guessing. Coin flip. You wasted everyone's time.
AUC of 0.7: decent. Better than random, usable with some caution.
AUC of 0.8: good. Most production models sit around here.
AUC of 0.9 and above: very good. The model is genuinely doing something useful.

{{< diagram-roc >}}

The reason AUC is better than accuracy is that it evaluates the model across all possible thresholds at once. It does not care where you drew the line. It just asks: is the model, in general, ranking the churners above the non-churners? If it is, you have something worth using.

---

## What 0.91 actually means

It does not mean the model is right 91% of the time. People always assume this and it is almost never what AUC means.

What it means is: if you take one user who churned and one who did not, the model will correctly rank the churner as higher risk 91% of the time. That is a very good model. Not perfect, nothing is, but good enough to be genuinely useful.

In practice, you take your full user base, run the model, get a probability score for every user, sort them from highest to lowest churn risk, and target the top 10%.

{{< diagram-ranked-list >}}

These are the users who look most like past users who churned. Your win-back campaign goes here. You do not need the model to be perfect. You just need it to do better than picking randomly. AUC of 0.91 clears that bar comfortably.

---

## The thing that will eventually break your model

Models drift.

User behaviour changes. Your product changes. A campaign runs and changes how people interact with the app. The model you trained six months ago is looking at the world as it was, not as it is.

This means two things.

First, check the AUC periodically on new data. If it starts dropping, the model is going stale. Retrain it.

Second, the first version you build is not the final version. It is a starting point. You learn from what it gets wrong, you add features, you retrain, you improve. Some people want the model to be a permanent answer. It is not. It is a living thing that needs attention. Like most things in analytics.

---

## The bit I want you to remember

The model does not tell you what to say to the users it flags. It does not design the campaign. It does not decide what offer to make.

It tells you where to look.

The top 10% of users on that ranked list are the ones who most need a conversation. What that conversation looks like is still a human decision.

The machine learned who your best customers are and who is about to stop being one. What you do with that is still on you.
