---
title: "The Leaky Bucket Problem"
date: 2026-05-30
categories: ["Analytics"]
tags: ["funnels", "conversion", "product analytics", "user behaviour"]
description: "Your conversion rate is 3.2%. That number tells you almost nothing. Here is what to look at instead."
draft: false
---

You open Swiggy. You are hungry.

You scroll through restaurants. You click on one. You look at the menu. You add something to cart. You see the delivery fee. You look at the total. You close the app and eat whatever is in the fridge.

This happens millions of times a day. And somewhere in a dashboard, it shows up as a drop in the funnel.

That entire sequence — open, browse, click, add, checkout, order — is a funnel. The question that matters is not how many people ordered. It is at which step most of them left.

---

## What a funnel actually is

A funnel is just a way of counting how many people make it from one step to the next.

You start with everyone who could potentially do the thing. You end with the people who actually did it. Every step in between is a place where some of them left.

The shape is always the same — wide at the top, narrow at the bottom. The interesting part is not the shape. It is where the narrowing happens fastest.

{{< diagram-funnel >}}

---

## Why your overall conversion rate is a lie

3.2%. That is your conversion rate. Users who opened the app and then placed an order.

That number is true. It is also nearly useless on its own.

Because 3.2% could mean a hundred different things. It could mean most people drop off immediately after opening the app. It could mean they get all the way to the checkout screen and then leave. It could mean they drop off evenly across every stage. Each of these is a completely different problem requiring a completely different fix.

Optimising for the overall rate without knowing where the drop happens is like a restaurant knowing their table occupancy is low but not knowing if people are leaving before they sit down, after they see the menu, or when the bill arrives.

The number hides the story. The stages tell it.

---

## Where people actually drop off

{{< diagram-funnel-stages >}}

Look at the drop between each stage, not just the start and end.

A 60% drop from browsing to clicking a restaurant is a different problem from a 60% drop from cart to payment. The first one is a discovery or relevance problem — people are not finding what they want. The second is a friction or trust problem — they want it but something stopped them at the last step.

Same percentage, completely different cause, completely different fix.

The stage with the biggest drop is almost never the last one. It is usually somewhere in the middle, where people had enough interest to get there but not enough conviction to continue. That middle stage is where the product is failing to make its case.

---

## The drop you should worry about vs the drop you cannot fix

Not all drop-off is created equal.

Some drop-off is structural. A certain percentage of people who open a food delivery app are just browsing with no real intention to order. They will never convert. That is not a problem to solve, that is the nature of the top of the funnel.

Some drop-off is fixable. If people are leaving because the delivery fee only appears at checkout, or the estimated time jumped from 30 minutes to 55 minutes, or the payment page errored out — those are solvable problems. You can measure them, fix them, and watch the drop rate change.

The distinction matters because a lot of analytics energy gets spent trying to reduce drop-off that cannot be reduced, while fixable problems sit untouched because nobody looked at the right stage.

---

## What the funnel does not tell you

The funnel tells you where people left. It does not tell you why.

A 70% drop at the cart stage could mean the delivery fee was too high. It could mean the estimated time was too long. It could mean the user got distracted by a message. It could mean they found a better option somewhere else.

The funnel gives you the question. The answer requires something else — session recordings, user research, a survey, or just talking to someone who actually left.

This is the part that gets skipped. The data tells you what happened. The why is still on you.

---

## The bit worth remembering

Your conversion rate is a summary. It summarises a process that has multiple steps, each of which can fail for different reasons.

The analysts who improve conversion rates are not the ones who look at the summary number and try to move it. They are the ones who look at each stage, find the one that is leaking most, understand why it is leaking, and fix that specific thing.

The bucket is always leaking somewhere. The question is which hole to plug first.

Most people look at how much water is left. The useful question is where it is going.
