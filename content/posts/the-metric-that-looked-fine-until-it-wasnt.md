---
title: "The Metric That Looked Fine Until It Wasn't"
date: 2026-05-10
categories: ["Analytics"]
tags: ["anomaly detection", "dashboards", "data quality", "metrics"]
description: "The metric dropped 40%. You were right to panic. Except you weren't. On sanity checking numbers before you tell anyone about them."
draft: false
---

The dashboard showed a 40% drop in sessions overnight.

You checked it once. You checked it again. You opened another tab and checked the same number from a different report. Still 40%. You sent a message to your team. Someone called it a P1. A meeting got scheduled for 9am.

The answer, when it came, was that the previous Sunday was a long weekend in three cities. Sessions always drop on long weekends. They had dropped the same amount the month before. Nobody had panicked then because nobody had been watching that closely.

This is not a story about incompetence. This is a story about what happens when you look at a number without enough context to know what it means.

---

## The problem with percentage changes

A 40% drop sounds catastrophic. Whether it actually is depends entirely on what you are comparing it to and what the baseline variation looks like.

If your metric swings 30% week on week on a normal week, a 40% drop is worth a second look but not a P1. If your metric is stable within 5% week on week, a 40% drop is genuinely alarming.

The number alone tells you nothing. The number in context tells you everything.

This is why the first question when something looks wrong is never "what happened" but "is this actually wrong."

{{< diagram-timeseries >}}

The chart above shows the same data at two zoom levels. Zoomed in to 7 days, it looks like a disaster. Zoomed out to 30 days, it looks like a Tuesday.

---

## The usual suspects

Before you escalate anything, run through this list. In roughly the order you should check them.

**Day of week effect.** Most metrics have a weekly pattern. Sessions are lower on weekends. Orders spike on paydays. If your drop happened on a Sunday, check what last Sunday looked like before assuming something broke.

**Public holidays and events.** One long weekend can halve your daily numbers in certain cities. If you are looking at city-level data this is even more pronounced. Always check the calendar before checking the code.

**Denominator shift.** A conversion rate drop can mean fewer conversions. It can also mean more sessions with the same conversions. The rate went down but nothing actually got worse. Check both the numerator and denominator separately before reading the combined metric.

**Data pipeline lag.** Some metrics take time to fully populate. Yesterday's numbers at 8am are not the same as yesterday's numbers at 6pm. If you are looking at recent data, check whether the pipeline has finished running.

**Report filter change.** Someone changed a filter somewhere. A date range got shifted. A segment got accidentally applied. These things happen more often than anyone admits. Check whether the query or report definition changed recently.

---

## The three questions

Before you tell anyone about an anomaly, ask yourself three things.

**Is this comparison fair?** Are you comparing like for like? Same day of week, same time period, no holidays or events in the mix?

**Is this outside normal variation?** What does the metric usually look like over 30 days? Is this drop within the range of normal swings, or genuinely outside it?

**Does it show up in related metrics?** If sessions dropped 40%, did orders also drop? Did conversion rate hold steady? A real problem usually shows up in more than one place. An artefact usually does not.

If you can answer all three and the number still looks wrong, then it is probably worth escalating. If any of the three has a simple explanation, resolve that first.

---

## When it actually is real

All of the above assumes the anomaly has an innocent explanation. Sometimes it does not.

A real problem tends to have a few characteristics. It shows up across multiple metrics, not just one. It does not have an obvious calendar explanation. It started at a specific point in time that corresponds to something — a deployment, a campaign launch, a partner integration change.

The investigation process is the same either way. You are just looking for a different answer at the end.

The difference between a false alarm and a real incident is not in how you investigate. It is in what you find.

---

## The thing I want you to remember

Being wrong about a number being wrong is still being wrong.

Escalating a false alarm costs time, credibility, and meeting slots that nobody gets back. The analyst who called three P1s that turned out to be long weekends will find that people stop taking the fourth one seriously.

The sanity check is not pessimism. It is the thing that makes your actual alerts meaningful.

When you have done the checklist and the number is still wrong, people will believe you. Because you are the person who checks before they speak.

The metric looked fine until it wasn't. Make sure you know which one you are dealing with before you tell anyone about it.
