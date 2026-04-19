# Case Study: PR Outreach Prompts

## Result
**60% journalist acceptance rate** within 3 months of launch — built from scratch, run entirely solo, replacing an outsourced vendor charging $400/month with inconsistent results.

---

## Background

BeamJobs had previously outsourced PR to a vendor who produced low-level results (~10 success rate/month for 100 pitches). I was brought in to own it from the ground up.

The core challenge: journalist queries on platforms like HARO and PressPulse require fast, credible, publication-ready responses. The prompt needed to produce pitches that journalists could lift directly into their articles — no sales language, no fluff, no generic advice.

I also uploaded examples of past pitches that had actually been featured by journalists to give the model calibration data on voice and tone, rather than describing style abstractly.

---

## What failed first

**`prompt_v1_monolithic.md`** — The original prompt tried to handle everything in one pass: evaluate the query, research a data point, write the pitch, format it for email. It worked sometimes but produced inconsistent tone and would occasionally ignore the word limit or slip into promotional language. No rubric meant no reliable quality floor.

---

## What changed

Split the problem. The prompt's job became singular: produce a journalist-ready pitch response that passes a specific 7-point rubric. Style calibration was handled by feeding example pitches as context. Structure was made adaptive rather than rigid — the model was told to choose the best flow for each query rather than follow a fixed template.

Key additions in **`prompt_v2_final.md`**:
- Explicit mission with 6 numbered goals
- Style calibration instruction: mirror voice from examples, not structure
- Output behavior rules: no preamble, no commentary, pitch content only
- 7-point quality rubric covering relevance, authority, tone, structure, readability, formatting, and professional fit
- "Pitch twisting" concept: answer adjacent queries when the angle is relevant (e.g., a food blogger pitching a healthy workplace query)

**`prompt_v3_lean.md`** is a deliberately stripped-down version — persona-first, strict 100–150 word limit, no rubric. Interestingly, both versions worked well. The lean version was faster to iterate with; the detailed version produced more consistent quality at scale.

---

## Key observation

Adding a rubric as part of the prompt — essentially giving the model a self-check before outputting — was the single biggest quality improvement. Before the rubric, outputs varied widely. After, quality variance dropped significantly and the 60% acceptance rate stabilized.

---

## Files

| File | Description |
|---|---|
| `prompt_v1_monolithic.md` | Original prompt — did too much at once, inconsistent results |
| `prompt_v2_final.md` | Final structured system prompt with rubric — used at scale |
| `prompt_v3_lean.md` | Lean version — persona-first, strict word limit |
