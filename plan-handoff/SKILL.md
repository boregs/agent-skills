---
name: plan-handoff
description: Turns an approved plan into a step-by-step execution script for a weaker, lower-effort model that will implement it. The planner resolves every decision, edge case, and failure mode up front so the implementer only follows steps. Use when the user approves a plan in plan mode, or asks for a handoff, execution script, or implementation steps for another model.
---

# Plan handoff

## Goal

When the user approves a plan, produce a self-contained execution script. The model that implements it is weaker and runs at lower effort, so it must not have to decide, infer, or anticipate errors. All of that thinking happens now, in the planner.

## Inputs

- The approved plan.
- The codebase and environment, which you can inspect now.
- Decisions and constraints the user stated during planning.

## Process

1. **Close open questions.** List every decision the plan leaves open (naming, library choice, approach, order). Decide each one. If a decision needs the user, ask before writing the script.
2. **Gather the facts the implementer would have to discover.** Read the code now and collect exact file paths, function and class names, signatures, the current code to change, and the commands to run. Never write "find the file that handles X".
3. **Think through failure.** For each step, work out what can go wrong (missing file, failing build, unexpected output, conflicting code) and write the exact remedy. If no safe remedy exists, write a stop condition.
4. **Write atomic steps.** One action per step, in execution order, in imperative mood. Give the exact path, the exact change (a code block when it is more than one line), the command that verifies it, and the expected result.
5. **Write stop conditions.** State when the implementer must stop and report back to the user instead of improvising.
6. **Test the script as the weaker model.** Reread it with no context from this conversation. Rewrite any step that needs a choice, an inference, or a judgment call. Remove vague words such as "appropriate", "as needed", "if necessary", "similar", and "etc.".
7. **Deliver** the script in the format below.

## Output format

Deliver one markdown document that makes sense without this conversation:

1. **Goal:** two sentences at most.
2. **Decisions already made:** each choice with its final answer, so the implementer does not reopen it.
3. **Prerequisites:** the exact state required before step 1, with a command to check it.
4. **Steps:** numbered. Each step has:
   - **Action:** what to do.
   - **Where:** exact file path or command.
   - **Change:** the exact code or text.
   - **Verify:** the command to run and the expected output.
   - **If it fails:** the exact remedy, or `STOP and report`.
5. **Out of scope:** what the implementer must not touch or add.
6. **Final verification:** the commands to run and the expected results.
7. **Done when:** a checklist the implementer can tick without judgment.

## Rules

- Do not delegate analysis. If a step requires comparing options, the planner already compared them.
- Do not leave placeholders such as `TODO` or `<choose>`.
- Prefer exact code over a description of code.
- Keep each step small enough to verify on its own.
- If the plan changes after the handoff is written, rewrite the affected steps and recheck the ones that follow.

## Final checks

- Could a model with no memory of this conversation follow every step without choosing anything?
- Does every step have a verification and a failure path?
- Are all decisions, paths, names, and commands explicit?
- Did you inspect the codebase instead of guessing paths or signatures?
