# Bonus Exercise: Adversarial Prompting

## The challenge

The file `fake_ai_output.md` contains a simulated AI response to a data analysis request on today's NHANES dataset. The response is realistic — it uses correct terminology, cites plausible numbers, and reads as authoritative.

It also contains errors.

Your task is **not** to find the errors by reading carefully. Your task is to **write prompts that would cause an AI to expose the errors itself.**

---

## Why this matters

AI outputs that contain errors usually don't announce themselves as wrong. They sound confident and complete. The skill is not spotting errors through expertise alone — it's knowing what to ask in order to surface problems the AI didn't volunteer.

---

## Instructions

Work in your team. You have the codebook, the dataset, and an AI tool.

**Step 1 — Read the output** (3–5 min)

Read through `fake_ai_output.md`. Note anything that seems off, surprising, or worth checking. Don't verify anything yet — just flag your suspicions.

**Step 2 — Write adversarial prompts** (10–15 min)

For each suspicion, write a prompt designed to get AI to reveal whether the claim is correct. Paste the prompt into your AI tool along with the codebook and relevant data.

Some prompting strategies that work well here:

- *"What are the limitations of [specific claim]?"*
- *"Please verify [specific value/claim] against the codebook."*
- *"Recompute [derived value] from the raw data and compare to what's reported."*
- *"What assumptions does [recommendation] rely on? Are those assumptions valid for this data?"*
- *"A reviewer has flagged [claim] as potentially incorrect. What would you say in response?"*

You don't have to find every error. Focus on writing prompts that are as targeted and specific as possible — vague prompts will get vague responses.

**Step 3 — Discuss** (5 min)

- Which prompts were most effective at surfacing problems?
- Which errors were easiest to expose? Which were hardest?
- What does this tell you about what to check by default in any AI-assisted analysis?

---

## Going further

- Try the same adversarial prompts on a different AI tool. Does it catch the same problems?
- Write a prompt that would catch all the errors in a single pass. Is that possible?
- Think about your own research data: what would an adversarial prompt look like for an analysis you've run recently?
