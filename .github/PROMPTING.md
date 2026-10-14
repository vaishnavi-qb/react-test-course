# Prompt-Based Learning Guide

Use an AI assistant as a tutor. You write the code. Paste the prompts from each exercise as they are — do not fill in blanks.

Each exercise issue has three ready prompts under **Use these prompts**:

1. **Explore** — paste first, before you change code  
2. **Plan** — paste next, when you are ready to implement  
3. **Review** — paste after you finish, with your diff available  

## How to use a prompt

1. Open your AI assistant in this repository (Cursor, Copilot Chat, Claude, etc.).
2. Copy the whole text inside the ` ```text ` block.
3. Paste it and send. Do not edit the prompt.
4. Follow the hints. Write the code yourself.
5. Run the checks listed in the exercise.

## Starter prompt (optional)

If you want a tutor setup before Exercise 01, copy this as-is:

```text
Act as a patient senior React tutor for this clothing-store repository. Do not edit files or paste a full solution unless I explicitly ask. Prefer one hint at a time. Keep advice consistent with the existing Vite frontend and Express backend. When I paste an Explore, Plan, or Review prompt from an exercise issue, follow that prompt exactly.
```

## Follow-ups (copy as-is when stuck)

```text
Give me one hint only for the next step. Do not show the final code. Tell me which file to look at and what to check.
```

```text
Explain the current behavior as a short sequence of events using the real files in this repo. Do not edit files.
```

```text
Review my current git diff only. Map each exercise step to evidence in the diff. List anything missing. Do not edit files.
```

## Rules

- Paste the exercise prompts without changing them.
- Do not paste `.env` contents, tokens, cookies, or secrets.
- You own the final code: you should be able to explain every change.
