# Case Study: Job Coaching Product — System Prompt for Claude-Powered Resume Editing

## Result
A live, revenue-generating BeamJobs product (generating $5,000/month by the third month) used across all clients. The step-locked workflow reduced editing time significantly — editors move through structured revisions without losing context or skipping steps. Migrated from ChatGPT to Claude after observing meaningfully better context retention across complex multi-step tasks.

---

## Background

BeamJobs offers a job coaching service where editors work with clients to revise and tailor resumes. The challenge was building a system prompt that could guide an editor through a complex, multi-step workflow — direction setting, gap analysis, rewriting, truth-checking, grading — without losing context between steps or requiring the editor to re-explain the situation at each stage.

The prompt needed to behave like a senior colleague: structured enough to be consistent across clients, flexible enough to adapt to each candidate's background, and strict enough to never invent or embellish candidate experience.

---

## What failed first

An earlier version of this prompt was tested on ChatGPT. It struggled with two things:

1. **Context dropping** — in long sessions with multiple document inputs (original resume, LinkedIn, older resumes, kickoff notes), ChatGPT would inconsistently apply earlier context to later steps, requiring the editor to re-paste information.
2. **Step bleeding** — without explicit step-locking, the model would sometimes attempt to complete multiple steps at once, reducing quality in each.

The same prompt on Claude performed significantly better on both counts — it retained client context across the full session and respected step boundaries reliably. This was the primary reason for migrating the job coaching product to Claude.

---

## Key design decisions

**Step-locking:** The prompt is structured as 9 explicit numbered steps. The model is instructed to present each step one at a time and wait for input before proceeding. This prevents the model from racing ahead and ensures the editor stays in control of the workflow.

**Explicit anti-hallucination rules:** Every step that involves writing includes a hard rule: *Do NOT invent or make up material about the candidate or the candidate's experience.* This is repeated at Steps 3, 7, and 8 — the three steps where the model is generating content. Repetition is intentional; in long sessions, single-mention rules get deprioritized.

**Editor-in-the-loop design:** The prompt positions Claude as a supporting tool, not the final decision-maker. Step 5 explicitly states: *"Always assume the human editor makes final wording decisions."* This keeps accountability with the editor and reduces over-reliance on model output.

**Built-in output formatting for downstream use:** Step 6 (Changes Made) is explicitly formatted for direct copy-paste into Notion for client delivery. The prompt instructs the model to write in second person, active voice, no bolding — ready for handoff without editing.

**Rubric-based grading:** Steps 5 and 9 include letter grading with explicit criteria. Grading serves as a forcing function — it surfaces remaining risks and gaps rather than letting the session end on a vague "looks good."

---

## Key observation

The migration from ChatGPT to Claude wasn't just an API swap — it was driven by a specific behavioral difference. Claude's stronger context retention across long, document-heavy sessions made it materially better for this use case. The same prompt that produced inconsistent results on ChatGPT worked reliably on Claude without structural changes.

This reinforced a broader principle: **prompt design has to account for how a specific model tends to behave.** The right model for a task isn't always the most capable model in general — it's the one whose behavioral tendencies align with what the task requires.

---

## Files

| File | Description |
|---|---|
| `prompt.md` | Full system prompt — 9-step guided resume editing workflow |
