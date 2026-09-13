# tonight. — a date night finder

A three-screen interactive mock-up: tell it how much time and money you have and where you are, and it opens up concrete date ideas for tonight — one shown in full, with the alternatives still visible beside it.

**Live prototype:** https://blakebaird2.github.io/DateNight/
**Repo:** https://github.com/BlakeBaird2/DateNight

## 1. Need, persona, capability, value

**Need.** When it's time to plan a date, the energy to come up with something new is already gone, so they default to the same few spots or an old saved post.

**Persona.** Works and takes classes on a shifting weekly schedule with a tight, variable budget, and is often deciding the night before whether a date is doable or suddenly free with no plan for the evening.

**Capability.** Find a specific date idea that fits their time, budget, and location right now.

**Fundamental value.** Confidence. The user gets to enjoy the date, rather than spend it wondering whether they picked the right plan.

## 2. The three screens

| Screen | Job | Why it earned the slot | Design question |
|---|---|---|---|
| 01 Landing | Signal the core value and primary capability in five seconds, nothing competing. | The only screen a first-timer sees before deciding whether to continue. | Capability: five-second test. |
| 02 Set your night | Show time, budget, and location being entered and specific ideas coming back. | It's the mechanism the whole app promises; without it the other two are a headline and a result. | Capability: "What would you tap first?" |
| 03 Your options | One idea in detail with visible alternates beside it. | Where need, capability, and value meet, and where "guide, not verdict" either holds or breaks. | Value: "What one or two words describe the value?" |

## 3. Feedback question plan

Written to ask later — not asked yet. Each prediction is tied to a specific part of the prototype.

| Group | Question (as I'd say it) | Prediction | What the prediction rests on |
|---|---|---|---|
| Need | "Last time you were trying to figure out what to do for a date, what did you end up doing?" | They name somewhere they've already been, or something generic like food and a movie — not a new idea they found. | The premise behind the landing screen, that defaulting to the familiar is the real behavior rather than a lack of places to go. |
| Value | "If this made picking something easier, what one or two words describe what you'd get out of it?" | Something near "confidence," but they may say "time," which would mean the value is landing as efficiency rather than confidence. | Screen 03 showing alternates beside the detailed idea — if that reads as a shortcut rather than reassurance, I'd expect a time-related answer. |
| Persona | "How often does this come up, and what are you usually doing when it does?" | Every week or two, usually the night before or the afternoon of, in between work and class. | The persona assumption that these decisions happen last-minute under time pressure, which is what the short time and budget inputs on Screen 02 are built around. |
| Capability | "I'm going to show you this screen for five seconds, then hide it. What does this product do?" *(Landing)* | They say it finds date ideas, but may not mention time, budget, and location — which would mean the subhead is too visually subordinate to the hero. | The landing screen's hero, affordance sentence, and subhead, and whether the subhead is carrying the three inputs or being skipped. |

## 4. Design justification and first read

**The affordance sentence.** The landing screen's job rests on one sentence — **"Set your night, see your options."** — paired with the single CTA beneath it, "Show me what's possible." Everything else on that screen (the "Stress less. *Connect more.*" hook above it, the subhead naming time, budget, and area, the "Provo & Utah County" location line) exists to support that sentence rather than compete with it.

Opened the live URL cold, as a first-time visitor:

**Does the landing screen signal the capability and value before reading?** Yes. One full-bleed image, one two-line hook, one affordance sentence, one subhead, one CTA. There is no second capability, nav bar, or competing call to action.

**Does everything on the landing screen earn its place?** Yes. The supporting content is the location line and the subhead, both of which qualify the promise rather than compete with it. The subhead is the element most at risk — it carries the three inputs, and if it reads as decorative it stops doing that job, which is what the Capability question is designed to test.

**What's grouped, and by which Gestalt principle?** On Set your night, the four inputs (time, budget, interests, area) each sit in their own bordered block with a divider rule between them — **common region** and **proximity** tell the eye these are one related decision, not four unrelated settings. On Your options, the alternates share one repeated card style and sit in their own column, separated from the single detailed card by **proximity** (spatial gap) and **similarity** (identical card treatment) — that pairing signals "these are the alternatives to that one" without a label saying so.

**Do screens 2 and 3 stay on mission, and can you get back to Landing from everywhere?** Yes on both. Screens 2 and 3 only show the filtering and decision flow — no settings, account, or unrelated content. Every screen carries the "tonight." wordmark wired to return home, and screens 2 and 3 also have an explicit "← Back to start" button.

**What did the AI initially get wrong, and what changed?** The first AI output (commit `2c9b569`) shipped four screens instead of three: a gallery of every matching idea, and a separate screen for one idea's detail. That split broke the grouping the capability depends on — comparing an idea against its alternatives meant leaving the idea entirely, so "compare" and "commit" were never spatially or visually connected. The two things that belonged together, a chosen idea and what it was chosen over, had no shared grouping at all.

I merged the gallery and detail screens into one (commit `e3df82d`): one chosen idea in full detail with two or three alternate cards beside it on the same screen, no scrolling. Picking an alternate swaps it into the detail position and the others stay put, so comparing and committing happen in one glance instead of two navigations.

A second, smaller revision followed from reviewing the merged flow: the progress label read "Step 1 of 2" on Set your night and then nothing at all on Your options, so the counter opened and never closed. A user had no confirmation they had reached the end of the flow. Adding "Step 2 of 2" to the options screen completes that signal.

**Which design question motivated the change?** The Value question on Screen 03. The prototype's whole claim is that it opens up options rather than deciding for you. A screen that shows one idea alone, with the alternatives one navigation away, signals a decision handed down — which would have made the honest answer to "what value do you see" something closer to "convenience" than "confidence."

### Before and after

| | Before (`2c9b569`) | After (`e3df82d`) |
|---|---|---|
| **Screens** | Four: Landing, Set, Options gallery, Idea detail. | Three: Landing, Set, Options. |
| **Comparing vs. committing** | Two separate screens — picking an idea navigated away from the list you were comparing it against. | One screen — the chosen idea and its alternatives are grouped together; picking an alternate swaps it in place. |
| **Progress signal** | "Step 1 of 2" on Set your night, nothing on the screens after it. | Counter completes: "Step 1 of 2" then "Step 2 of 2." |

Named in course terms: the original split violated **proximity** and **common region** between a decision and the alternatives it was being weighed against. The issue was not that it looked incomplete — it was that the two things that belonged together, a chosen idea and what it was chosen over, had no shared grouping at all.

## Notes

- Built with an AI coding agent (Claude) as a Claude Design canvas (`Date Night Finder.dc.html`), which renders client-side via `support.js` — no build step.
- `index.html` is a thin redirect to `Date Night Finder.dc.html` so the root URL loads the app directly.
- An earlier concept built in a separate Claude Design project ("NextDate") led with "Plan less. Connect more." and a remembered-preferences feature. Both framed the product as planning *for* the user, which contradicted the intent that it guide rather than replace the user's own planning. The brief was rewritten around "Stress less. Connect more." before this repo was created.
