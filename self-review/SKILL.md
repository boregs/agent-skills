---
name: self-review
description: Critiques and corrects its own answer, plan, code, or design before delivering it to the user, flagging flaws, weak assumptions, and risks. Use whenever the user asks for a plan, solution, code, architecture, or analysis, or asks to review, critique, or validate its own answer before returning it.
---

# Self-review

## Goal

Before delivering any answer or plan, give an honest critique of your own draft, fix the real problems, and only then return the final version to the user.

## Inputs

- The user's request (task, question, or goal).
- Your internal draft of the answer, plan, or code.
- Constraints stated in the conversation (stack, deadline, project standards).

## Process

1. **Draft** the complete answer without delivering it yet.
2. **Reread the original request** and list what the user actually asked for, including explicit constraints.
3. **Critique the draft as a skeptical reviewer.** Look for:
   - Requirements from the request that are missing or only half met.
   - Assumptions you made that the user never stated.
   - Logic errors, code errors, or factual errors.
   - Edge cases and failure scenarios that are not handled (empty or invalid input, concurrency, network errors).
   - Security, performance, or maintainability risks.
   - Unnecessary complexity: is there a simpler solution?
   - Points you cannot verify with what you have on hand.
4. **Classify each problem** as critical (invalidates the answer), important (makes it considerably worse), or minor.
5. **Fix** the critical and important problems in the draft. Fix minor ones only if it is cheap.
6. **Reread the corrected version** one last time to make sure the fix did not introduce a new problem.
7. **Deliver** using the format below.

## Output format

1. The final answer, plan, or code, already corrected.
2. A short **Review** section with:
   - **What I fixed:** changes made after the critique (omit if there were none).
   - **Assumptions:** what I assumed and the user should confirm.
   - **Remaining risks:** what could still go wrong or was not verified.

Keep the Review section lean, at most one line per item.

## Final checks

- Does the final answer cover everything that was asked?
- Was anything invented to fill a gap? If something was not verified, is it stated in the Review section?
- Were the problems found during the critique fixed or declared, rather than hidden?
- Did the review avoid turning into an excuse to pad the answer with unimportant caveats?
