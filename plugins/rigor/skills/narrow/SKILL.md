---
name: narrow
description: Cuts a task prompt down to the question that matters before it runs. It names the real question behind the prompt, what a top professional in the field would refuse to do, what can be cut or deferred, and the smallest result that would settle the question. Then it rewrites the prompt to ask for only that and lists what it cut. Use when the user runs /narrow, asks to scope down, focus, trim or simplify a task, says a request is too big or sprawling, or asks what really matters in it.
argument-hint: <the prompt or task to narrow>
---

# Narrow

Make the task smaller without making it easier. The skill produces a tighter prompt; it doesn't do the work.

## What makes this work

- One real question. Most sprawling prompts serve a single decision or outcome. Naming it shows which parts serve it and which ride along.
- The professional's refusals. A practitioner shows judgment in what they decline to do as much as in what they do: premature work, someone else's job, questions the available material can't answer.
- The smallest result that settles it. A minimal deliverable with a clear sense of "enough" beats a complete one that buries the answer.
- Cuts in the open. The rewrite lists every cut, so the user can put any of them back.

`deepen` makes the same task more rigorous. Running `narrow` first and then `deepen` on its output works well.

## Input

The prompt to narrow is the skill's argument. With no argument, use the task the user most recently asked for in this conversation; if there is none, ask for one. Don't start the task.

## Step 1: Name the field and the professional

Pick the narrowest field whose standards will judge the result, and name the practitioner: "a staff engineer scoping a migration", "a newspaper editor assigning a story". "An expert" is too vague. Answer the rest as that person.

## Step 2: Answer the four questions

Each answer must point to specific parts of the prompt.

1. **What is the real question?** State in one sentence the decision or outcome that everything else serves. If the prompt holds two unrelated questions, say so and pick the one the user needs answered first.

2. **What would they refuse to do here?** Name the parts that are premature, out of scope, someone else's job, or unanswerable with the available material, and say why for each.

3. **What can be cut or deferred?** Name the deliverables, coverage words ("all", "every", "comprehensive"), polish and side quests that don't change the answer to question 1.

4. **What is the smallest result that would settle it?** Describe the minimal deliverable and how to tell it's enough: a single number, a yes or no with evidence, one working path through the code, a one-page draft.

## Step 3: Rewrite the prompt

Write a prompt that asks only for the real question and the smallest result that settles it. Keep the user's goal, hard constraints and voice. End the prompt with one line listing what was deferred, so the user can pick it up later.

## Output

Name the field and professional in one line. Then give the four answers, numbered, in two to four sentences each. Put the rewritten prompt in a fenced block so the user can copy it, and end with one line offering to run it. Don't run it until the user says to.

## Failure modes

- Cutting the hard part: keeping the easy work and deferring the part that answers the question.
- Changing the goal. A narrower prompt answers the same question with less work.
- Dropping the user's constraints. Deadlines, formats, audiences and explicit requirements stay unless the user agrees to drop them.
- Cutting silently. Every cut must appear in the deferred line.
