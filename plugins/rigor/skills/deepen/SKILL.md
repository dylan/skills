---
name: deepen
description: Deepens a task prompt before it runs. It names what a top professional in the field would do that the prompt doesn't ask for, the rawest material they would start from, the methods and tools they would use, and a check outside the model and the user that would show the result is right. Then it rewrites the prompt to ask for exactly that. Use when the user runs /deepen, asks to deepen, sharpen or level up a prompt or task, asks how an expert would approach something, or wants expert-grade work rather than a longer answer.
argument-hint: <the prompt or task to deepen>
---

# Deepen

Make the task deeper without making it bigger. The skill produces a better prompt; it doesn't do the work.

## What makes this work

Each part of the method closes a gap between an amateur request and professional work.

- Depth, not breadth. The rewrite keeps the original goal and scope and adds no deliverables. It changes how the work is done and what counts as done.
- Diagnosis first. The user sees the four answers before the rewrite, and the rewrite asks only for what those answers justify.
- A named professional. Asking what a top practitioner would do brings in the steps they take for granted, which the user didn't know to ask for.
- Raw material. Summaries, articles and earlier answers carry someone else's framing and errors. Starting upstream lets the work find what the summary dropped.
- Named methods and tools. A method with a name can be run, checked and repeated; "analyze it carefully" can't.
- An outside check. The model grading its own work proves nothing, and neither does the user eyeballing it. Only a check that can disagree with both of them turns an opinion into a result.

## Input

The prompt to deepen is the skill's argument. With no argument, use the task the user most recently asked for in this conversation; if there is none, ask for one. Don't start the task.

## Step 1: Name the field and the professional

Pick the narrowest field whose standards will judge the result, and name the practitioner: "a forensic accountant", "a senior SRE who runs incident reviews", "a structural editor at a literary press". "An expert" is too vague. If the task spans fields, pick the one where a mistake would cost the most. Answer the rest as that person.

## Step 2: Answer the four questions

Make every answer concrete enough to act on tomorrow by naming the sources, files, techniques, tools and numbers.

1. **What would they do that the prompt doesn't ask for?** Look for the step a professional treats as routine and an amateur skips: defining the question before answering it, checking the base rate, deciding how to measure success, finding prior work, ruling out the boring explanation first. The step must serve the same goal; a new deliverable adds breadth, not depth.

2. **What raw material would they start from?** Go upstream of what someone has already digested: the dataset behind the chart, the filing behind the news story, the source code behind the docs, the transcript behind the summary, the user's own logs instead of a blog post about the topic. Name the source and where to get it. If it can't be reached from here, say so and name the closest source that can.

3. **What methods and tools would they use?** Name the technique, instrument, library, standard or procedure: "a Kaplan-Meier curve with R's `survival` package", "`git bisect` with a scripted repro", "a five-whys pass on the incident timeline". "Research it", "analyze the data" and "follow best practices" don't count.

4. **What, other than the model or the user, would show the result is right?** Name a check that can fail: a test suite, a measurement, a reproduced number, a known-answer case, a published standard, a prediction that comes true, a real user's behavior, a second independent source. Self-review, "looks correct" and another model's opinion don't count. State the pass condition.

## Step 3: Rewrite the prompt

Write a prompt that asks for exactly what the four answers describe. It keeps the original goal, scope, constraints and voice, and it says:

- what to start from (answer 2)
- how to work, including the professional's extra step (answers 1 and 3)
- what counts as done, as a pass/fail condition (answer 4)

Cut whatever the answers made obsolete. Keep the prompt as short as it can be; a paragraph or a short list is usually enough.

## Output

Name the field and professional in one line. Then give the four answers, numbered, in two to four sentences each. Put the rewritten prompt in a fenced block so the user can copy it, and end with one line offering to run it. Don't run it until the user says to.

## Failure modes

Before writing the rewrite, check the answers for these:

- Generic answers, such as "consult experts", "use reliable sources" or "validate the results". Replace each with the specific step, source or check.
- Scope creep: the rewrite asks for more things when it should ask for better work on the same thing.
- A digest passed off as raw material. A review article, a Wikipedia page or a vendor's summary is still a digest.
- A circular check: anything that comes down to the model's judgment or the user's approval.
- Doing the task. The deliverable is the four answers and the rewritten prompt.
