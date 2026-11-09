---
name: prove
description: Finds and runs the check that could show a result is wrong. It splits a finished result, claim, fix or answer into testable claims and picks a check for each that can fail and doesn't rely on the model or the user. It writes each pass condition down before running the check, runs it, and reports passed, failed or unverified with evidence. Use when the user runs /prove, asks to prove, verify or check that something is right, asks "how do we know this works", or wants evidence about finished work instead of reassurance.
argument-hint: <the result, claim or change to check>
---

# Prove

Show whether a result is right with a check that could have shown it wrong. The skill produces evidence, not a review.

## What makes this work

- Testable claims. Nobody can check "the fix works". Anyone can check "the request that returned 500 now returns 200, and the existing suite still passes".
- An outside check. Neither the model rereading its own work nor the user eyeballing it can disagree with the result. Running code, taking a measurement, reproducing a number or reading the primary source can.
- Pass conditions written first. Writing down what counts as a pass before seeing the outcome keeps the goalposts from moving to fit it.
- Running the check. A check that is only described proves nothing, so an unrun check leaves its claim unverified.

## Input

The skill's argument names the result to check: a claim, a diff, an answer, a document or a number. With no argument, check the most recent result in this conversation, including the agent's own. If there is nothing to check, ask what to check.

## Step 1: State the claims

Rewrite the result as a short list of testable claims, splitting compound ones. Mark the load-bearing claims, whose failure would make the result wrong or harmful. Check those first and skip trivia.

## Step 2: Pick a check for each claim

Pick the strongest check that can run from here. Roughly from strongest to weakest:

1. **Execute:** run the test suite, the program, the query or a scripted repro.
2. **Measure:** time it, count it, diff the output or profile it.
3. **Known-answer case:** feed it an input whose correct output is already known.
4. **Primary source:** the spec, dataset, filing or source code, quoted with its location.
5. **Independent second source:** one that didn't come from the first.

Before running anything, write the pass condition next to each check: the exact output, number, status or quote that counts as a pass.

The check must not share the result's source of error. A test written from the same misunderstanding as the code will agree with the mistake. So will a mock that stands in for the thing being checked, or the same model working out its own answer again.

## Step 3: Run the checks

Run every check that can run here, and capture the command and the relevant output. Some checks need credentials, hardware, production data or a person. Mark those claims unverified and say exactly what would run the check.

## Output

Lead with the verdict in one line: how many load-bearing claims passed, failed or remain unverified. Then give a table with one row per claim, listing the claim, the check, the pass condition and the result, with failures first. Under the table, give the evidence for each failure and each unverified claim: the command and output, or the quote and where it came from.

Don't fix failures unless the user asks. End with one line offering to.

## Failure modes

- A check that can't fail, such as asserting that a function returns something, testing a mock, or grepping for code that was just written.
- A moved goalpost: rewriting the pass condition after seeing the result.
- Unverified reported as passed. If a check didn't run, its claim didn't pass.
- Checking the easy claims: verifying three trivial ones and skipping the claim the result depends on.
- Self-agreement: any check that comes down to the model's judgment or the user's approval.
