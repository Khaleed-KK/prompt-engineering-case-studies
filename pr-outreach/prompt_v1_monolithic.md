# PR Outreach Prompt — v1 (Monolithic, Deprecated)

**Status:** Deprecated  
**Problem:** Tried to evaluate query relevance AND draft the pitch in one pass. Produced inconsistent tone, occasional word limit violations, and would sometimes slip into promotional language. No quality rubric meant no reliable output floor.

**What replaced it:** v2 (structured system prompt with rubric) and v3 (lean, constrained version)

---

*Note: v1 was an earlier, undocumented iteration that combined query evaluation with pitch writing in a single prompt. The core failure mode was inconsistent output quality — without a rubric or explicit style calibration, the model had no self-check mechanism before outputting. This was resolved in v2 by separating style calibration, adding a 7-point rubric, and making output behavior rules explicit.*
