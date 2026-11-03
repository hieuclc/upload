# Read-aloud script: Tutorial Part 2 (about 23 minutes)

Every lab follows the same three blocks:
1. **Introduce the lab**: what the task is and why it matters.
2. **Key points: prompt and files**: what the agent is given, and what it is not.
3. **Questions to observe the output**: the questions on the slide ("Track" and "Review" steps) plus the extra ones below. Ask them aloud, then look at the real output together.

**Slide** is the slide to show. **Say** is what you read out. **Demo** is what you do on the agent screen. Figures marked "example" come from an earlier run saved in `tutorial/solutions/`. Your live result may differ: read the real output. The questions stay the same.

| Segment | Min | Running total |
|---|---|---|
| Introduction | 3 | 3 |
| Lab 6 + 7: MoSCoW and change requests | 10 | 13 |
| Lab 8: acceptance criteria | 6 | 19 |
| Lab 9: Definition of Done | 4 | 23 |

Two points to repeat in **every** lab:
- **Who checks the output?** We do. The agent can sound confident and still be wrong, even when it reviews its own work.
- **Why give it context?** The agent only knows what is in the files it reads. For everything else, it guesses.

## Demo preparation (before the session)

- One model and one agent for the whole session. Write down the model name.
- Every run in a **new session**, clean repo, empty `tutorial/workspace/`. The exception is Lab 8: both steps run in the **same** window.
- Paste the prompt **verbatim** from `tutorial/starter/prompts/`. Do not retype it.
- Do one full dry run beforehand. The result is your fallback (already in `tutorial/solutions/`).
- If the live output differs from the example, that is **normal**. Use it as a teaching point and do not re-run.
- If the agent fails or is slow: open the matching file in `solutions/` and say "this is an earlier run".

---

## Introduction (3 min)

**Slide:** "Prioritize and manage scope with AI".

**Say:**
"Today we are not learning how to write prompts. We are learning how to **review the output** of an agent. To review it, you need to know what the agent was **given**. So in each lab I will show the prompt and the files it reads first, then run it."

"There are two kinds of input. The **prompts**: six files, 07 to 12, in `tutorial/starter/prompts`. And the **context files** in `tutorial/starter`: `backlog.yaml` (15 user stories, capacity 50 points), `stakeholder_notes.md` (Founder, Operations, Marketing), `change_requests.yaml` (two new requests), `business_rules.md` (three promo rules), `DEFINITION_OF_DONE.md` (six criteria), `pr_sf06.md` (a pull request with its CI log)."

"Every lab runs the same loop: the agent works, **we check**, then we add context. Results go to `tutorial/workspace`."

---

## Lab 6: MoSCoW

### 1. Introduce the lab

**Slide:** "Lab 6: Prioritise with MoSCoW" (show the steps and output files, then go to the prompt slides).

**Say:**
"SoopiFood has 15 user stories and room for 50 points. We rank them with MoSCoW: Must, Should, Could, Won't. We do it twice. Round 1, the agent sees only the backlog. Round 2, we give it what the stakeholders said. The question for the whole lab: **what did the agent not know in round 1?**"

### 2. Key points: prompt and files (round 1)

**Slide:** "Lab 6 · Round 1 · prompt" (`07_moscow_round1.md`).

**Say:**
- "Prompt `07` gives the release goal, the four MoSCoW definitions and the constraints: fit 50 points, roughly 60/20/20, use the whole budget."
- "The agent **may read only `backlog.yaml`**: the 15 stories and their points. Not the stakeholder notes."
- "If a reason is a guess, it must write `assumption`."
- "It must output tables with id **and** title: one row per story, a summary by category, and a met / not met line per constraint."

**Demo:** run prompt 07, open `workspace/moscow_round1.md`.

### 3. Questions to observe the output

**Say:**
- "Add up the points. Is it exactly 50 out of 50? Does the self-check agree?" (Example: Must 29, Should 10, Could 11.)
- "Which reasons are assumptions?" (Example: promo code is a Should, `helps growth, not blocking`; cash on delivery is a Must, `Hanoi customers expect cash`.)
- "Where do promo codes and cash on delivery land?"

**Who checks, and why context:**
"The agent marks every constraint 'Met', but **we** add it up. Correct arithmetic is not a correct decision. Now open `stakeholder_notes.md`: the Founder says the launch campaign is built on promo codes; Operations says about 70% of first-time customers pay cash. The agent never saw those sentences. Without them we cannot tell which assumption is right."

### 2. Key points: prompt and files (round 2)

**Slide:** "Lab 6 · Round 2 · prompt" (`08_moscow_round2.md`).

**Say:**
- "Prompt `08` adds one file: `stakeholder_notes.md`, three short quotes."
- "Same constraints. For every story whose priority changes, the agent must name the note that caused it."
- "Three tables: changes from round 1, final allocation, and new allocation (points and % per category)."

**Demo:** run prompt 08, open `workspace/moscow.md`.

### 3. Questions to observe the output

**Say:**
- "Is every move explained by a note? (Example: promo code Should to Must from the Founder; rate and review Could to Should from Marketing.)"
- "Which moves are still assumptions? Who decides those?"
- "Is the new allocation still 50 out of 50? (Example: Must 32, Should 10, Could 8.)"

**Wrap up:** "With context, each change has a source. What the agent still assumes is a **decision for a person**."

---

## Lab 7: Change requests

### 1. Introduce the lab

**Slide:** "Lab 7: Handle Change Requests".

**Say:**
"The plan is agreed at 50 out of 50. Then two requests arrive. Allergen information from Legal: 2 points, **mandatory by law**. Split the bill from Marketing: 8 points, wanted for the campaign, but the campaign can run without it. The capacity does not change. So every added point must be **paid for**."

### 2. Key points: prompt and files

**Slide:** "Lab 7 · prompt" (`09_change_requests.md`).

**Say:**
- "Prompt `09` reads two files: `change_requests.yaml` and the plan from Lab 6, `workspace/moscow.md`. That is why Lab 7 needs Lab 6's output."
- "For each request: a MoSCoW priority and why. If it adds effort, say exactly what is demoted or dropped."
- "Output: a decision table, changes to the plan, final allocation of all stories and both requests, and a new allocation."

**Demo:** run prompt 09, open `workspace/scope_changes.md`.

### 3. Questions to observe the output

**Say:**
- "What pays for each added point? Add the numbers again." (Example: allergen info Must, paid by demoting one-tap reorder SF-09 to Won't; split the bill Won't; allocation 34 / 10 / 6.)
- "If the agent said yes without removing anything, the plan is over capacity. That is **scope creep**."
- "Which choice is the agent's assumption? Who confirms it?"

**Wrap up:** "Which story to drop is often the agent's own guess. It is **our** decision, with the stakeholders. Accepting a new request is a trade-off you can see."

---

## Lab 8: Acceptance criteria

### 1. Introduce the lab

**Slide:** "Write and verify acceptance criteria with AI", then "Lab 8: Write Acceptance Criteria".

**Say:**
"A user story says what the customer wants, not exactly what 'done' means. Acceptance criteria in Gherkin do. We write them for SF-06, the promo code, in **one agent window and two steps**. Step 1, the agent writes with only the story. Step 2, we give it the business rules and it reviews and rewrites its own file. The question: **where does each number come from?**"

### 2. Key points: prompt and files (step 1)

**Slide:** "Lab 8 · Round 1 · prompt" (`10_criteria_writer.md`).

**Say:**
- "Prompt `10` reads **no file**. It has only the user story."
- "Exactly three scenarios: one `@happy`, one `@error`, one `@edge`, with concrete values in VND and dates."
- "Anything it assumes goes in one `# assumption` line at the top."
- "Look at the box on the right of the slide: `business_rules.md`. The writer is **not given** it."

**Demo:** run prompt 10, open `workspace/discount.feature`.

### 3. Questions to observe the output

**Say:**
- "Every number in a `Then` step: does it come from the rules, or was it guessed?"
- "Which are listed as assumptions, and which are not?"
- "The file looks complete: valid Gherkin, concrete values, three tags. Does that mean it is right?" (The code, percentage and expiry date are invented.)

### 2. Key points: prompt and files (step 2)

**Slide:** "Lab 8 · Round 2 · prompt" (`11_criteria_review_rewrite.md`).

**Say:**
- "**Same window.** The agent keeps its own file in memory."
- "New context: `business_rules.md`. R1: minimum order 100,000 before the discount. R2: a discount never exceeds its cap and the delivery fee is never discounted. R3: a code is valid up to and including its expiry date. These are the **only source of truth**."
- "Step 1: review the file against the rules into `review.md`, a table of at most three rows."
- "Step 2: rewrite to `discount_v2.feature`: exactly three scenarios, one per rule, each on its boundary."

**Demo:** run prompt 11, open `workspace/review.md` and `workspace/discount_v2.feature`.

### 3. Questions to observe the output

**Say:**
- "Is the review real? Does it point out real problems?" (Example: totals ignore the delivery fee; cap and last valid day untested; some values invented.)
- "Does each of R1, R2, R3 have exactly one scenario on its boundary?" (Example: 99,999; 200,000 with a cap; the expiry date.)
- "The agent checked its own work. Pick one finding and verify it yourself."

**Demo:** calculate the R2 scenario live: 20% of 200,000 is 40,000, capped at 30,000; 200,000 minus 30,000 plus a 15,000 delivery fee is **185,000**. Compare with the file.

**Who checks, and why context:**
"The review sounds convincing, but nobody independent has checked it. So **we** check."

**Slide:** "Takeaway: give the context up front".
**Say:** "Step 1 had no rules, so the agent invented values and forgot the delivery fee. Step 2 had the rules, so it could fix them. **On a real project, put the rules in the first prompt.**"

---

## Lab 9: Definition of Done

### 1. Introduce the lab

**Slide:** "Check the Definition of Done with AI", then "Lab 9: Audit the Definition of Done".

**Say:**
"Acceptance criteria belong to one story. The Definition of Done applies to **every** story. Pull request #42 says 'Ready to merge, story is done'. Is it? We ask the agent to audit the PR against our six criteria. The question: **is every status backed by a quoted line, not a claim?**"

### 2. Key points: prompt and files

**Slide:** "Lab 9 · prompt" (`12_dod_audit.md`).

**Say:**
- "Prompt `12` reads two files: `DEFINITION_OF_DONE.md` (D1 to D6) and `pr_sf06.md` (the PR description, the CI table, the diff)."
- "One row per item: met, not met, or cannot tell, plus the **exact line of evidence**."
- "The author's own claims do not count as evidence."
- "At the end: a verdict, and at most three next steps."
- "On the slide, look at the input: the PR says 'all acceptance tests pass', but the CI table shows 13 scenarios, 1 failed."

**Demo:** run prompt 12, open `workspace/dod_audit.md`.

### 3. Questions to observe the output

**Say:**
- "For each status, find the quoted line in the PR yourself. Is it really there?"
- "D1: did it tick from the author's claim or from the CI log?"
- "D2: is Copilot counted as a team reviewer?"
- "D3: was 'SKIPPED' read as 'passed'?"
- "D5: does it catch the problem only visible in the diff, the float division on money?"
- "From the next-steps table, would the author know what to do first?"

(Example: 1 of 6 items met, so not Done.)

**Who checks, and why context:**
"Pick one cell, say D1, and find the quoted line in the CI log yourself. If it is there, you can trust that cell. The context here is the **evidence**: the CI log and the diff, not the author's description."

---

## Closing and submission (1 min)

**Slide:** "Lab Submission".

**Say:**
"Four labs, two lessons. **First**, agent output looks reasonable from the first try, so a person must always check: add up the points, work out one number, find one line of evidence. Even when the agent reviews its own work. **Second**, when the agent is wrong it is usually missing context, and the fix is to give it the right context."

"Submit **all outputs of Labs 6 to 9**: `moscow_round1.md`, `moscow.md`, `scope_changes.md`, `discount.feature`, `review.md`, `discount_v2.feature`, `dod_audit.md`, plus your prompt log."

## If something goes wrong

- **Output differs from the example:** normal. Read the real output; the questions do not change.
- **The agent reads a file it should not in round 1:** start a new session and repeat "Do not read any other file".
- **The agent is slow or fails:** open the matching file in `solutions/` and say it is an earlier run.
- **Short on time:** skip the live calculation in Lab 8, then the next-steps question in Lab 9.
