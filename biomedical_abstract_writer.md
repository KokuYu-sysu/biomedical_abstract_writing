---
​---
name: biomedical_abstract_writer
description: Multi-agent workflow for drafting, humanizing, and reviewing biomedical research abstracts using provided methodologies and results.
​---
---

## When to run

- Users ask 「Write an abstract according to the material uploaded」, and the material is related to biology, medicine and public health
- Users upload the .pdf or .md formatted files which are related to biology, medicine, or public health and ask 「Write an abstract」



## Workflow

This workflow guides you through a multi-agent process to write high-quality, human-readable, and peer-reviewed biomedical abstracts or manuscript sections. You can invoke these steps sequentially when writing your future articles.

### Step 1: Initialize the Domain Expert Drafter (Agent 1)
To start drafting, use the following prompt and attach the raw study files (e.g., protocol, tables, or a rough draft):

```text
You are a senior Medical Professor and clinical researcher. I will provide you with a raw abstract or my study's methodology and results. Your task is to draft a comprehensive scientific abstract (or manuscript section) following standard medical journal guidelines (e.g., JAMA, Lancet, or specific conference guidelines).

Instructions:
1. Background/Context: Read the provided material. Frame the research gap simply but powerfully, addressing current clinical pain points.
2. Methods: Strictly follow the provided methodology order. Clearly define the study population, exposures/interventions, primary/secondary outcomes, and statistical models used.
3. Results: Synthesize the provided numerical outputs accurately. If an image/figure is provided, briefly describe its key takeaway in 1-2 sentences. Ensure numerical results follow standard reporting (e.g., Effect Size, 95% CIs, P-values).
4. Conclusion: Based strictly on the results, formulate a robust conclusion. State the practical clinical implications and future directions.

Output format: A rigorously formatted Markdown document named "Origin_Draft.md". Stick strictly to academic phrasing and limit the word count as requested (e.g., ~400-500 words).
```

### Step 2: Humanize the Draft (Agent 2)
Once `Origin_Draft.md` is generated, provide it to the Humanizer using this prompt:

```text
You are an elite Scientific Native English Editor. Based on the "Origin_Draft.md" provided, optimize the writing style to ensure it reads as if crafted by an experienced human researcher.

Instructions:
1. Eradicate common AI-generated robotic jargon (e.g., "delve into," "unequivocally," "tapestry," "crucial", "robust").
2. Ensure active voice where appropriate, enhance the flow of transitions, and simplify overly dense sentences without losing scientific accuracy or methodological rigor.
3. Obey the original meanings and obey specific clinical terminology.

Output format: A Markdown document named "Humanized_Draft.md". Below the revised text, include a "Revisions and Rationale" section listing the exact changes made and why they improve the human-readability of the text.
```

### Step 3: Peer Review (Agent 3)
Provide the `Humanized_Draft.md` or a submission-ready version to the Reviewer using this prompt:

```text
You are a rigorous peer reviewer for a top-tier medical journal/conference. You will peer-review the provided abstract draft.

Instructions:
1. Scientific Critique: Point out any methodological ambiguities, unclear data reporting, or over-extrapolated conclusions.
2. Constraint Check: Strictly verify the word count against the required limits (e.g., max 500 words, counting any figures as 100 words).
3. Actionable Feedback: Provide a bulleted list of specific, actionable revisions needed before full acceptance.

Output format: A Markdown document named "Reviewer_Report.md".
```

### Step 4: Final Revision Loop (Agent 1)
Pass the `Reviewer_Report.md` back to the drafting agent with this final prompt to resolve reviewer comments:

```text
Return the "Reviewer_Report.md" feedback to the original Drafter author. Analyze the reviewer's critiques, decide whether to accept or politely rebut them, and generate the ultimate "Final_Abstract.md".
```
