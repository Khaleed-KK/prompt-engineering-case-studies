# Case Study: OpenAI to Claude API Migration

## Background

BeamJobs' WordPress integration originally ran on the OpenAI API. As we began using Claude for other internal projects — specifically the job coaching product — we observed consistent behavioral differences that made Claude a better fit for our use case.

The migration involved swapping the API, recalibrating temperature, and verifying that output quality matched or improved on what we had with OpenAI.

---

## Why we switched

The clearest signal came from building client questionnaires. With ChatGPT, the model would repeatedly drop important context mid-task — we'd give it a full client profile and it would ignore parts of it, requiring manual correction afterwards. With Claude, it retained the full context of each client's situation across the entire task with significantly less editing needed.

This wasn't a quality difference in the sense of "Claude writes better sentences." It was a behavioral difference in how the model holds and applies context across a complex, multi-step task — which is exactly what resume editing requires.

---

## Temperature calibration

OpenAI and Claude handle temperature differently. A direct port at the same temperature value produces different output characteristics.

For our WordPress integration, we calibrated Claude's temperature to **0.7** — high enough to introduce the creative variation we wanted (Claude at lower temperatures can be overly conservative in phrasing), but controlled enough to maintain consistency across client outputs.

The target wasn't to make Claude behave exactly like GPT. It was to match the *output characteristics* we needed — consistent structure, appropriate variation, no hallucinated credentials — while taking advantage of Claude's stronger context retention.

---

## Key observation

Migrating between models isn't just an API swap. Each model has different defaults, different sensitivities to temperature, and different behavioral tendencies under the same prompt. A prompt that works well with GPT-4 may need structural changes with Claude — not because one is better, but because they weight instructions differently and have different failure modes.

Understanding this distinction — and testing for it rather than assuming a direct port will work — is what made the migration smooth.

---

## What this connects to

This migration informed how I think about all prompt work: the model is part of the system, not just an interchangeable component. Prompt design has to account for how a specific model tends to behave, not just what you want the output to look like.
