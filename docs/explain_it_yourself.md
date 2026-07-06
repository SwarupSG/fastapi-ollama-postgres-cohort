# Explain It Yourself — Written Assignment

You've been answering **Defend-It** out loud. This is the written version: **one short explanation per module, in your own words.**

The goal is *not* to describe every line. A senior developer reading new code doesn't explain all 25 lines — they find the **one line that is the point of the module** and explain that. That's the skill you're practising here: separating the signal from the scaffolding.

Do this right after you finish each module, while it's fresh — it takes about five minutes.

---

## What a good answer looks like

- **It names one line.** Not the whole file — the single line (or tiny block) that *is* this module's new idea. If you can't pick one, you haven't found the fundamental yet — re-read, or ask Gemini "which one line is the point of this module?"
- **It's in your own words.** Don't paste the README's sentence back. Explain it the way you'd explain it to the next person in the cohort who's stuck.
- **It would make sense to someone who hasn't seen the code.** That's the test.

You may use Gemini to *check* your explanation ("is this right?") — but write your version first. The point is that *you* generate it.

---

## How the hints fade

Early modules give you a hint about where to look. From Module 4 on, the hints get lighter; by Modules 7–8 there's no hint at all — finding the load-bearing line yourself *is* the assignment. That's deliberate: by the end you're doing unaided what the instructor demonstrated at the start.

For every module, answer these five:

1. **The one line I think is load-bearing** (paste it, with `file:line`):
2. **What it does, in my own words** (2–3 sentences):
3. **What I predicted before running vs. what actually happened:**
4. **Why is it written this way — and what would a typical tutorial add here that we deliberately did *not*?**
5. **My Defend-It answer** (the question at the bottom of the module's README):

---

## Module 01 — Hello FastAPI
*Hint: look for the line that connects a web address (a URL) to a Python function.*

1.
2.
3.
4.
5.

## Module 02 — Post + Pydantic Echo
*Hint: look at what the `ask` function receives. One small piece of that line is doing a lot of invisible work.*

1.
2.
3.
4.
5.

## Module 03 — Call Ollama
*Hint: find the line where your app stops talking to itself and starts talking to another program.*

1.
2.
3.
4.
5.

## Module 04 — System Prompt
*Lighter hint: something new was added to the list of messages sent to the model. What, and where?*

1.
2.
3.
4.
5.

## Module 05 — Save to Postgres
*Lighter hint: one line makes this the first module where closing the app doesn't lose your data.*

1.
2.
3.
4.
5.

## Module 06 — Read History
*Lighter hint: the "write" verb from Module 5 has a "read" counterpart. Find it.*

1.
2.
3.
4.
5.

## Module 07 — Refactor into Layers
*No hint. But a warning: the diff is big and nothing the app DOES has changed. So your "load-bearing line" question is different here — what got shorter, and why is that the point?*

1.
2.
3.
4.
5.

## Module 08 — Configuration
*No hint. Find the line that decides where a critical setting comes from — and what happens when it's missing.*

1.
2.
3.
4.
5.

---

**Submitting:** keep this file with your answers in your own cohort folder and bring it to office hours, or submit however your instructor asked. It's also a genuinely useful revision sheet later — eight modules, eight sentences, the whole app.
