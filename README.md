# Prompt Engineering Case Studies

A collection of production prompt engineering work from my role at [BeamJobs](https://www.beamjobs.com) — a resume and career tools SaaS company.

Each case study documents the problem, what failed, what changed, and what the result was. These are not toy examples — all prompts ran in production, connected to real tools (Clay.com, Zapier, Claude API, OpenAI API), and produced measurable outcomes.

---

## Case Studies

### 1. [PR Outreach — From Inconsistent to 60% Acceptance Rate](./pr-outreach/)
Built and iterated the system prompt powering BeamJobs' journalist outreach program from scratch. Went from inconsistent results with an outsourced vendor to a consistent **60% journalist acceptance rate** (60/100 pitches placed) within 3 months. Documents v1 (monolithic, low confidence), v2 (structured system prompt with rubric), and v3 (lean, constrained version).

### 2. [Clay Backlink Pipeline — Chained LLM Steps for Outreach Automation](./clay-backlink-pipeline/)
Designed a 4-step chained pipeline where each LLM prompt takes output from the previous step: fit evaluation → keyword count → pitch paragraph 1 → pitch paragraph 2. Documents the original monolithic prompt that tried to do everything at once (and failed), and the final pipeline that processes **50–150 leads/week** with high-confidence outputs.

### 3. [Job Coaching Product — System Prompt for Claude-Powered Resume Editing](./job-coaching/)
Authored the system prompt governing BeamJobs' live job coaching product — a multi-step, step-locked Claude workflow that guides resume editors through structured revisions. Originally built for ChatGPT, migrated to Claude after observing better context retention across complex multi-step tasks.

From this experience, I learned that Claude 3.5 Sonnet often responds well to fewer examples and benefits strongly from explicitly structured prompts (like XML), while GPT-4 tends to be more flexible with natural-language instructions but still benefits from clear structure.

### 4. [API Migration — OpenAI to Claude with Temperature Calibration](./api-migration/)
Documents the process of migrating BeamJobs' WordPress integration from the OpenAI API to the Claude API, including temperature calibration to match and improve on existing output behavior.

---

## What these show

- Designing prompts that are part of larger automated systems (not one-off queries)
- Iterating from low-confidence to high-confidence outputs through structured debugging
- Understanding behavioral differences between models and calibrating accordingly
- Decomposing a complex task (evaluate + draft + send) into sequential, single-responsibility steps
- Writing system prompts that govern behavior across multiple clients and use cases
