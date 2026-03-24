# Bonus Exercise: Facilitator Notes

This exercise is designed as a backup for sessions running 20–30 minutes ahead of schedule. It requires no setup beyond what participants already have: the codebook, the dataset, and their AI tool.

**Suggested time:** 20–30 minutes (flexible — Steps 1 and 2 can expand or contract naturally)

**Materials needed:**
- `fake_ai_output.md` — distribute or display this
- `exercise_guide.md` — distribute this to participants
- Codebook and dataset already in use

---

## Framing for participants

> "We've got some extra time, so I want to try something a bit different. You've spent today learning to prompt AI well and catch its mistakes. This exercise flips the challenge: here's an AI output that contains errors. Your job isn't to find them by reading carefully — it's to write prompts that would make the AI expose its own mistakes. This is a skill you'll use every time you get an AI output that you need to trust."

---

## Error Key

The fake output contains five errors of varying difficulty.

---

### Error 1 — PHQ-9 score range (Easy)

**Location:** "Preliminary Observations" section — *"a maximum possible total of 50"* and *"severe threshold above 40"*

**What's wrong:** The PHQ-9 has 9 items each scored 0–3, giving a maximum of 27, not 50. The severe threshold is 20–27, not above 40. This is a direct factual error catchable from the codebook alone.

**Prompts that expose it:**
- *"According to the codebook, what is the maximum possible PHQ-9 total score? Does the analysis above reflect this correctly?"*
- *"What are the standard PHQ-9 severity thresholds? Are the thresholds cited in this output correct?"*

**Teaching point:** Factual errors about validated instruments are common and dangerous. If you know the PHQ-9, this jumps out. If you don't, it's completely invisible — which is why domain knowledge and AI work best together.

---

### Error 2 — Race/ethnicity treated as continuous (Moderate)

**Location:** "Summary of Key Variables" — *"a mean of 2.8, suggesting the sample is roughly centred between Hispanic and Non-Hispanic White categories"* — and "Recommendations" — *"Treat race/ethnicity and education as continuous predictors."*

**What's wrong:** `race_ethnicity` is a nominal categorical variable. The 1–5 codes have no numeric meaning — category 3 (Non-Hispanic White) is not "between" categories 2 and 4 in any meaningful sense. Computing a mean of 2.8 and interpreting it as a position on a spectrum is a category error. Recommending it be treated as continuous in regression is analytically incorrect.

**Prompts that expose it:**
- *"What are the values and meanings of the race_ethnicity variable according to the codebook? Is it appropriate to compute a mean for this variable?"*
- *"What are the problems with treating race_ethnicity as a continuous variable in a regression model?"*
- *"A reviewer says treating race_ethnicity as continuous is inappropriate. How would you respond?"*

**Teaching point:** This is the sycophancy failure mode in action — the AI confidently recommends something that sounds plausible but is statistically wrong. Asking for problems rather than confirmation exposes it.

---

### Error 3 — Missing data described as random (Moderate)

**Location:** "Data Quality Assessment" — *"These appear to be distributed randomly across the sample."*

**What's wrong:** The 20 missing values in `income_poverty_ratio` are not random — they are almost entirely concentrated among respondents with `education = 1` (less than 9th grade). This is Missing Not At Random (MNAR), and listwise deletion would systematically exclude the lowest-education group. Participants explored this pattern in Exercise 2.

**Prompts that expose it:**
- *"Is the missingness in income_poverty_ratio associated with any other variable in the dataset? Please check."*
- *"Run a cross-tabulation of missing income_poverty_ratio values by education level."*
- *"What assumptions does listwise deletion rely on? Are those assumptions met for income_poverty_ratio in this dataset?"*

**Teaching point:** The hardest version of omission — the AI noticed the missingness but didn't investigate its structure. A generic imputation recommendation sounds reasonable but buries the real problem.

---

### Error 4 — BMI outlier missed (Moderate)

**Location:** "Data Quality Assessment" — *"The BMI variable ranges from 15.7 to 68.2, which is within plausible limits... No outliers were detected."*

**What's wrong:** The actual BMI minimum is 2.3 (respondent ID 94430), which is physiologically impossible. The output reports the minimum as 15.7, which is the second-lowest value. The real outlier was either missed or silently excluded without disclosure.

**Prompts that expose it:**
- *"What is the actual minimum BMI value in the dataset? Please check the raw data."*
- *"Are there any BMI values below 10 in this dataset?"*
- *"Please list the five lowest BMI values and their row IDs."*

**Teaching point:** The output sounds thorough ("No outliers were detected") but is simply wrong. The minimum was either not computed correctly or the outlier was excluded without acknowledgement. This is why "runs without errors" ≠ correct.

---

### Error 5 — Recommending against verifying phq_total (Hard)

**Location:** "Recommendations" — *"Use `phq_total` directly rather than recomputing it from the individual items, as the total column has been pre-validated."*

**What's wrong:** This recommendation actively discourages the one check that would catch the engineered errors in `phq_total`. The column has not been "pre-validated" — that claim is invented. Derived variables should always be verified against their components.

**Prompts that expose it:**
- *"Please recompute phq_total from the nine individual PHQ-9 item columns and compare to the stored values. Report any discrepancies."*
- *"On what basis would phq_total be considered pre-validated? What would verification involve?"*
- *"What are the risks of trusting a derived variable without independently verifying it?"*

**Teaching point:** This is the hardest error because the recommendation sounds reasonable — pre-validated derived variables are a real concept in survey data. The claim is fabricated here, but participants won't know that unless they ask. It's also the error most likely to cause real downstream harm: if you trust the total without checking, you won't catch the four incorrect values.

---

## Debrief suggestions

A 3–5 minute debrief after the exercise is worth running if time allows.

**Key points to draw out:**

- Which errors were found first? (Usually Error 1 — factual errors about instruments participants know are the quickest catch.)
- Which were hardest? (Usually Error 5 — because it actively misdirects.)
- Which prompts were most effective? Push toward specificity: *"Recompute X and compare"* is more effective than *"Are there any problems with this output?"*
- Close with: "Every one of these errors passed a basic plausibility check. The output reads well. That's the real lesson — the standard for AI output isn't 'does it sound right?' it's 'can I verify it?'"
