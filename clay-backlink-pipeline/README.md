# Case Study: Clay Backlink Pipeline — Chained LLM Steps

## Result
**50–150 leads processed per week** with high-confidence outputs (95%+ green confidence ratings in Clay.com), saving an estimated **2+ hours/week** of manual checking. Replaced a monolithic prompt that consistently produced low-confidence, mixed-task outputs.

---

## Background

BeamJobs runs an outreach program to acquire backlinks from relevant articles — pages that cover resumes, job applications, or career advice. The workflow involves:

1. Importing a list of article URLs from Ahrefs
2. Evaluating whether each article is a good fit for a backlink pitch
3. Counting resume-related keyword frequency as a relevance signal
4. Drafting a personalized first paragraph referencing a specific section of the article
5. Drafting a second paragraph with an editorial tool recommendation
6. Sending the pitch via Instantly.ai

The challenge was designing prompts that could do this reliably at scale — with high confidence outputs — across hundreds of URLs per week.

---

## What failed first

**`old_prompt_monolithic.md`** — The original prompt tried to evaluate fit AND draft the pitch in a single pass. This caused two problems:

1. **Low confidence outputs** — Clay.com's AI confidence scoring was consistently red/yellow. The model was splitting attention between evaluation logic and creative writing simultaneously, doing neither well.
2. **Mixed quality** — Some outputs were good, others ignored the word limit, used promotional language, or drafted pitches for articles that shouldn't have qualified.

The fix wasn't to make the monolithic prompt better. It was to decompose the task entirely.

---

## The pipeline design

Each step has a single responsibility. Output from one step feeds the next.

```
Step 1: Fit Check
↓ "Good Fit" or "Bad Fit"
Step 2: Keyword Count (only runs on "Good Fit" articles)
↓ Integer (total keyword occurrences)
Step 3: Pitch Para 1 (only runs if keyword count ≥ 3)
↓ 1–2 lines referencing a specific article section
Step 4: Pitch Para 2
↓ 1 paragraph with editorial tool recommendation + HTML link
```

Splitting evaluation from generation was the core insight. Once each prompt had one job, confidence scores jumped to 95%+ green.

---

## Key observations

**Single-responsibility prompts outperform multi-task prompts in automated pipelines.** When a prompt tries to evaluate and generate simultaneously, it produces inconsistent outputs because the two tasks have conflicting optimization targets — one rewards precision and binary thinking, the other rewards creativity and variation.

**Output format rules matter more in pipelines than in standalone prompts.** Because each step's output is consumed programmatically by the next step, strict output formatting (e.g., "output exactly 'Good Fit' or 'Bad Fit', no other text") is non-negotiable. Any deviation breaks the chain.

**Confidence scoring as a real-time eval.** Clay.com's AI confidence indicator served as an in-product eval signal — iterating the fit-check prompt until consistently hitting green (high confidence) was a practical stand-in for formal evals.

---

## Files

| File | Description |
|---|---|
| `old_prompt_monolithic.md` | Original prompt — evaluated and drafted in one pass, low confidence |
| `step1_fit_check.md` | Evaluates whether an article qualifies for a pitch |
| `step2_keyword_count.md` | Counts resume-related keyword frequency |
| `step3_pitch_para1.md` | Drafts personalized opening referencing a specific article section |
| `step4_pitch_para2.md` | Drafts editorial tool recommendation paragraph with HTML link |
