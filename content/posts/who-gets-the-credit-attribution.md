---
title: "Who Gets the Credit? On Attribution, Windows, and Dashboards That Lie"
date: 2026-04-05
categories: ["Analytics"]
tags: ["attribution", "analytics", "dashboards", "traffic"]
description: "A concept that sounds simple until your dashboard and reality stop agreeing with each other."
draft: false
---

There's a meeting I've sat in more than once where two teams are looking at the same campaign and arriving at completely different numbers.

Team A says the campaign brought in 10,000 users. Team B says 4,000. Both are using data. Both are confident. Someone inevitably says "can we align on a single source of truth" and everyone nods and nothing changes.

This is an attribution problem. And it's not a data quality problem, usually. It's a *definition* problem wearing a data quality costume.

---

## The basic idea

Attribution is just answering: *who gets the credit?*

Say a user sees a Meta ad on Monday. Does nothing. Searches on Google Tuesday, clicks through. Sees a Criteo retargeting banner on Wednesday. Still does nothing. Gets a push notification Thursday, ignores it. Then on Friday opens the app directly: organic: and finally converts.

{{< diagram-touchpoints >}}

Which channel gets the credit for that conversion?

Meta will say Meta. Google will say Google. Criteo will say Criteo. The CRM team will say the push notification warmed them up. And if you're pulling numbers from each platform's own dashboard, all five will show that conversion in their reports. Your total will add up to 500% of reality.

This is not a conspiracy. Each platform is applying its own attribution logic and counting what it can see. The problem is you're treating three different answers to three different questions as if they're the same answer to one question.

---

## The approaches people use

{{< diagram-models >}}

**Last touch**: whoever touched the user last gets full credit. In our example, Organic wins everything. Simple, clean, wildly unfair to Meta who started the whole thing. It's the equivalent of the guy who forwards a finished report to leadership and gets promoted while the analyst who built it remains invisible. (Not that this has ever happened to anyone I know.)

**First touch**: Meta gets full credit for the acquisition. Better for understanding where users are coming from. But it completely ignores Criteo's retargeting or the PN that kept the user engaged. Like giving your Class 1 teacher full credit for your MBA.

**Linear**: split 20% evenly across all five touchpoints. Democratic but a little naive. Meta's brand campaign and a Criteo banner are not doing the same job in the funnel.

**Time decay**: touchpoints closer to conversion get more credit. Organic and PN look great. Meta, who started the whole journey, gets 5%. Your top-of-funnel team will love explaining this in the next budget review.

**Data-driven**: use a model to figure out which touchpoints actually move the needle. Theoretically the best. Requires a lot of data and a lot of trust in the model. Also requires someone to explain it to a stakeholder at 10am on a Monday, which is its own category of suffering.

---

## The part nobody tells you

Here's what I've noticed: the attribution model matters less than you think. What matters more is *consistency*.

If you pick last-touch and stick with it, you can at least track trends over time. If you switch models every quarter because someone read an article, your historical data becomes useless and every review meeting turns into a methodology debate instead of a business conversation.

Pick something defensible. Document it. Make sure everyone is pulling from the same place. That's 80% of the battle.

The other 20% is a full-time job.

---

## The thing that actually breaks dashboards

The sneaky issue isn't which model you pick. It's the **attribution window**: how far back you look when deciding whether a touchpoint counts.

If your window is 7 days, a user who saw your ad on day 1 and converted on day 8 gets counted as organic. If your window is 30 days, that's an attributed conversion. Same user, same behavior, different number on your dashboard.

Now imagine two teams using different windows pulling from different platforms with different default settings. You don't get one source of truth. You get a choose-your-own-adventure where every team is technically correct and nobody agrees on anything.

I once spent a surprisingly long time trying to figure out why two reports on the same campaign were off by about 40%. The answer was a default attribution window difference between two tools. Not a bug. Not missing data. Just two systems being very precise about slightly different questions.

Anyway. That was a fun week.

---

## So what do you do

**Define before you build.** Before anyone touches a dashboard, get the team to agree on: what counts as a conversion, which touchpoints are in scope, what the attribution window is, and which tool is the system of record. Write it down. Put it somewhere people can find it. Revisit it when something breaks.

**Don't fight the platform numbers, contextualize them.** Google's numbers will always be higher than your internal numbers. That's expected: they're counting within their ecosystem. The question isn't "who's right" but "what question is each number answering."

**Be suspicious of round numbers.** If your report shows exactly 10,000 attributed conversions, something might be capped or defaulted somewhere. Real data is rarely that tidy.

**When two numbers disagree, find the third.** If Team A and Team B are both confident and both wrong, there's usually a third dataset sitting quietly that resolves it. It's not always obvious which one, but it exists.

---

Attribution doesn't have a correct answer. It has a *chosen* answer. The job is making sure everyone knows what was chosen and why, so the debates are at least about the right things.

The meetings still happen. But at least you know what you're arguing about.
