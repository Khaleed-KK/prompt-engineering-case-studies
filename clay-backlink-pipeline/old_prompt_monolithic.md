# Clay Pipeline — Original Monolithic Prompt (Deprecated)

**Status:** Deprecated  
**Problem:** Tried to evaluate article fit and draft the pitch in a single pass. Produced consistently low-confidence outputs in Clay.com (red/yellow confidence scores). The model was splitting attention between binary evaluation logic and creative pitch writing simultaneously — doing neither reliably.  

**What replaced it:** 4-step chained pipeline (steps 1–4)

---

## Original prompt

**Objective:**  
Evaluate whether a given article or webpage is a good fit for a backlink pitch promoting one or more tools from BeamJobs (e.g., AI Resume Builder, Resume Templates, or Cover Letter Generator).

**Primary Evaluation Criteria:**  
The article should be relevant to job seekers, especially those applying for jobs, building or improving resumes, or exploring career paths. Strong matches usually include a section on resumes or cover letters, offer resume tips or examples, or focus on career transitions.

**Resume Keyword Check:**  
Use the frequency of the word "resume" (or CV, curriculum vitae) as a signal. If "resume" appears 3 or more times, that's a strong indicator. However, the context still matters — the article must speak to job seekers, not just mention resumes in passing.

**Pitch Output Format:**  
Only output two short paragraphs. Do not write a full email. Use this structure:

> I recently came across your page, [Article Title] ([URL]), where you provide valuable resources, including [brief mention of the resume-related section].
>
> Would you consider adding a link to our [Tool Name] ([Tool URL]) in your article? It would add value by offering your readers a practical tool to [benefit].

**Tool Priority (Evaluate in This Order):**
1. AI Resume Builder — for articles helping users prepare resumes
2. Resume Templates — for articles about layout or design
3. Cover Letter Generator — for articles focused on cover letters

**If the Article Is Not a Good Fit:**  
Output a clear reason why the article is not relevant.

---

## Why this failed

The evaluation task (binary: fit or not) and the generation task (creative: draft a pitch) have conflicting optimization targets. Asking the model to do both in one pass produced outputs where the evaluation was sometimes uncertain and the pitch was sometimes drafted for articles that should have been rejected. Separating them into sequential single-responsibility steps resolved both problems.
