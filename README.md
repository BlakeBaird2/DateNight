# tonight. — a date night finder

A three-screen interactive mock-up: tell it how much time, money, and where you are, and it hands you one concrete date idea for tonight — with backups still visible, not just a list to keep scrolling.

**Live prototype:** https://blakebaird2.github.io/DateNight/
**Repo:** https://github.com/BlakeBaird2/DateNight

---

## 1. Need, persona, capability, value

**Need.** When it's time to plan a date, the energy to come up with something new is already gone, so they default to the same few spots or an old saved post.

**Persona.** Works and takes classes on a shifting weekly schedule with a tight, variable budget, and is often deciding the night before whether a date is doable or suddenly free with no plan for the evening.

**Capability.** Find a specific date idea that fits their time, budget, and location right now.

**Fundamental value.** *Confidence.* The user gets to enjoy the date, rather than spend it wondering whether they picked the right plan.

---

## 2. The three screens

| Screen | Job | Why it earned the slot | Design question |
|---|---|---|---|
| **01 Landing** | Signal the core value and primary capability in five seconds, nothing competing. | The only screen a first-timer sees before deciding whether to continue. | Capability: five-second test. |
| **02 Set your night** | Show time, budget, and location being entered and specific ideas coming back. | It's the mechanism the whole app promises; without it the other two are a headline and a result. | Capability: "What would you tap first?" |
| **03 Your options** | One idea in detail with visible alternates beside it. | Where need, capability, and value meet, and where "guide not verdict" either holds or breaks. | Value: "What one or two words describe the value?" |

---

## 3. Feedback question plan

Written to ask later — not asked yet. Wording is aimed at the persona above (a couple deciding a weeknight date), and each prediction is tied to a specific part of the prototype.

| Group | Question (as I'd say it) | Prediction | What it's testing |
|-------|---------------------------|------------|--------------------|
| Need | "When was the last time you two tried to figure out something to do on a weeknight — what actually happened?" | They'll describe 15–20 minutes of scrolling apps or group-texting friends, then defaulting to the same restaurant or staying in. | Whether the Landing → Set-your-night path actually short-circuits that scrolling loop, or just adds another app to check. |
| Value | "If tonight's plan were just handled for you, what's the one or two words for what that's worth? Why?" | "Less stress" or "actually present," not "cool app" or "convenient." | Whether "Stress less. Connect more." on the landing screen matches the value they'd name unprompted. |
| Persona | "How often does this come up, and what are you usually doing right before you'd open something like this?" | Weeknights after work, already tired, actively avoiding one more decision. | Whether the Set-your-night inputs (short time windows, modest budget) match real weekday constraints rather than an idealized weekend date. |
| Capability | "I'll show you this screen for five seconds — [Your options] — then hide it. What does this let you do?" | "Pick one specific thing to do tonight, with a backup," not "browse a list of restaurants." | Whether the detail-card + alternates layout on Screen 3 reads as one clear decision rather than a generic results list. |

---

## 4. Design justification and first read

**The affordance sentence.** The landing screen's entire job rests on one sentence — *"Set your night, see your options."* — paired with the single CTA beneath it, "Show me what's possible." Everything else on that screen (the "Stress less. Connect more." hook above it, the "Provo & Utah County" location line) exists to support that sentence, not compete with it.

Opened the live URL cold, as a first-time visitor, and answered these directly:

**Does the landing screen signal the capability and value before reading?**
Yes. One full-bleed photo, one two-line hook ("Stress less. *Connect more.*"), one headline ("Set your night, see your options."), one CTA. There is no second capability, nav bar, or competing call to action on that screen — the affordance sentence is the whole screen.

**Does everything on the landing screen earn its place?**
Yes — nothing competes with the primary job. The only supporting content is the location line ("Provo & Utah County"), which qualifies the promise rather than competing with it.

**What's grouped, and by which Gestalt principle?**
On **Set your night**, the four inputs (time / budget / interests / area) are each wrapped in their own bordered block with a divider rule between them — **common region** and **proximity** tell the eye these are one related decision, not four unrelated settings. On **Your options**, the alternates share one repeated card style and sit in their own column, separated from the single detailed card by both **proximity** (spatial gap) and **similarity** (identical card treatment) — that pairing signals "these are the alternatives to that one" without needing a label to say so.

**Do screens 2 and 3 stay on mission, and can you get back to Landing from everywhere?**
Yes on both. Screens 2 and 3 only ever show the filtering/decision flow — no settings, account, or unrelated content. Every screen carries the "tonight." wordmark wired to return home, and screens 2 and 3 also have an explicit "← Back to start" button.

**What did the AI initially get wrong, and what changed?**
The first AI output (commit [`2c9b569`](https://github.com/BlakeBaird2/DateNight/commit/2c9b5697dc4ee46fae53acca954374e7f2d32b1e)) shipped **four** screens instead of three: a full gallery of every matching idea, and a *separate* screen for one idea's detail. That split broke the grouping the capability depends on — comparing an idea against its alternatives required leaving the idea entirely, so "choose" and "compare" were never visually or spatially connected, which is exactly the kind of ungrouped, uncommitted decision the assignment brief warns against. It also left a stray "Step 1 of 2" label that undercounted the real number of downstream screens.

I merged the gallery and detail screens into one (commit [`e3df82d`](https://github.com/BlakeBaird2/DateNight/commit/e3df82d2446cfa683e8dd871b17c1e721f27c170)): one chosen idea in full detail, 2–3 alternate cards beside it, same screen, no scrolling. Picking an alternate swaps it into the detail position and the others stay put — so "compare" and "commit" now happen in one glance instead of two navigations. That also made the step counter correct for the first time, since the flow is now genuinely two steps past Landing.

**Before / after:**

| | Before ([`2c9b569`](https://github.com/BlakeBaird2/DateNight/commit/2c9b5697dc4ee46fae53acca954374e7f2d32b1e)) | After ([`e3df82d`](https://github.com/BlakeBaird2/DateNight/commit/e3df82d2446cfa683e8dd871b17c1e721f27c170)) |
|---|---|---|
| Screens | 4 (Landing, Set, Options gallery, Idea detail) | 3 (Landing, Set, Options) |
| Comparing vs. committing | Two separate screens — picking an idea navigated away from the list you were comparing it to | One screen — the chosen idea and its alternatives are grouped together; picking an alternate swaps it in place |
| Step counter | "Step 1 of 2" undercounted a flow with 3 screens after Landing | "Step 1 of 2" is accurate for the real 2-step flow (Set → Options) |

The problem, named in course terms: the original split violated **proximity/common region** between a decision and the alternatives it was being weighed against — "it looked incomplete" isn't the issue; the issue is that the two things that belonged together (a chosen idea and what it was chosen over) had no shared grouping at all.

---

## Notes

- Built with an AI coding agent (Claude) as a Claude Design canvas (`Date Night Finder.dc.html`), which renders client-side via `support.js` — no build step.
- `index.html` is a thin redirect to `Date Night Finder.dc.html` so the root URL loads the app directly.
- Not graded on code quality or visual polish — see the assignment brief for scope.
