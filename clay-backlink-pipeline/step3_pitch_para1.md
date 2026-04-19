# Step 3: Pitch Paragraph 1

**Pipeline position:** Step 3 of 4  

**Input:** Article URL (only receives articles that passed Steps 1 and 2)  

**Output:** 1–2 lines (max 25 words) referencing a specific article section 

**Purpose:** Personalized opening that shows the journalist the pitch writer actually read their article  

**Key design decision:** Fixed output template with one variable slot — reduces creative variance while maintaining personalization

---

#CONTEXT#
You will analyze a public web article to extract and generate a pitch opening. The article URL is provided in [URL]. The focus is on identifying resume, CV, cover letter, or job-application sections and highlighting where readers may struggle with practical implementation.

#OBJECTIVE#
Read [URL] and output 1–2 lines (max 25 words) that reference a specific section and concisely describe an implementation challenge, formatted exactly as requested.

#INSTRUCTIONS#
1) Access the article at [URL]. If the page is unreachable or paywalled, output nothing.

2) Identify explicit sections related to: resume, CV, cover letter, or job-application. Prefer clear section headers or anchored subsections; if multiple exist, choose the most substantial or concrete section.

3) For the chosen section, determine a likely reader implementation challenge (e.g., applying templates to unique backgrounds, quantifying impact, tailoring content without sounding generic).

4) Write 1–2 lines, total maximum 25 words, in a neutral, editorial, reader-focused tone.

5) Use this format strictly: "I liked how you covered {specific section or topic}. That's usually the moment when readers understand the advice yet still struggle to apply it to their own resumes."
   - Replace {specific section or topic} with the exact section name from the article.
   - Reference a concrete implementation challenge observed in that section.

6) Do not include any other commentary, metadata, disclaimers, or quotes beyond the single final line(s). Output ONLY the final line(s).

7) Word limit enforcement: Ensure total output does not exceed 25 words.
