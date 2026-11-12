# GEMINI.md

Rules for writing code in this project. Follow them on every task.
For trivial tasks (typo, rename), use judgment and skip the ceremony.

## 1. Think before coding
- State your assumptions before you write code. If unsure, ask.
- If there are multiple valid interpretations, list them and ask. Don't pick silently.
- If a simpler approach exists, say so and push back.
- If something is unclear, stop and name exactly what is confusing.

## 2. Keep it simple
- Write the minimum code that solves the request. Nothing speculative.
- No extra features, no abstractions for single-use code, no unrequested configurability.
- No error handling for scenarios that can't happen.
- Don't add new dependencies unless asked.
- If 200 lines could be 50, rewrite it.
- Check: "Would a senior engineer call this overcomplicated?" If yes, simplify.

## 3. Make surgical changes
- Edit only what the request requires. Every changed line must trace back to it.
- Don't reformat, rename, or "improve" adjacent code or comments.
- Match the existing style, even if you'd write it differently.
- Notice unrelated dead code? Mention it, don't delete it.
- Remove imports/variables/functions that YOUR change made unused. Leave pre-existing ones alone.

## 4. Work toward verifiable goals
Turn vague tasks into checkable ones:
- "Add validation" → write tests for invalid inputs, then make them pass.
- "Fix the bug" → reproduce it first, then make it pass.
- "Refactor X" → tests pass before and after.

For multi-step tasks, write a short plan first:
1. [Step] → verify: [check]
2. [Step] → verify: [check]

Don't say "done" until you've run the check. If you can't run it, say so and explain how I can verify it.

## 5. Report back
End each task with a short summary: what changed, which files, and anything you were unsure about.