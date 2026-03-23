# Workshop Dataset Codebook
## NHANES 2017–2018 Subset | N=350 | 20 variables

Source: National Health and Nutrition Examination Survey, 2017–2018 cycle.
CDC/National Center for Health Statistics. Freely available at wwwn.cdc.gov/nchs/nhanes.
This is a subset of 350 adult respondents aged 20–65.

---

| Variable | NHANES source | Type | Description | Values / Range |
|---|---|---|---|---|
| id | SEQN | integer | Unique respondent ID | — |
| age | RIDAGEYR | integer | Age at screening | 20–65 |
| sex | RIAGENDR | categorical | Sex of respondent | Male, Female |
| race_ethnicity | RIDRETH1 | categorical | Race/Hispanic origin | 1=Mex. American, 2=Other Hispanic, 3=NH White, 4=NH Black, 5=Other |
| education | DMDEDUC2 | ordinal | Highest education level | 1=<9th grade, 2=9–11th, 3=HS/GED, 4=Some college, 5=College+ |
| marital_status | DMDMARTL | categorical | Marital status | 1=Married, 2=Widowed, 3=Divorced, 4=Separated, 5=Never married, 6=Partnered |
| income_poverty_ratio | INDFMPIR | continuous | Family income ÷ poverty threshold | 0–5 (>5 coded as 5; higher = higher income) |
| hh_sz | DMDHHSZA | integer | [see codebook note] | 1–7+ |
| bmi | BMXBMI | continuous | Body mass index | kg/m²; typical adult range 15–60 |
| ever_smoked | SMQ020 | binary | Ever smoked ≥100 cigarettes | Yes, No |
| phq_interest | DPQ010 | ordinal | PHQ-9 item 1: little interest/pleasure | 0=Not at all, 1=Several days, 2=More than half, 3=Nearly every day |
| phq_depressed | DPQ020 | ordinal | PHQ-9 item 2: feeling down/depressed | 0–3 (same scale) |
| phq_sleep | DPQ030 | ordinal | PHQ-9 item 3: sleep problems | 0–3 |
| phq_tired | DPQ040 | ordinal | PHQ-9 item 4: fatigue | 0–3 |
| phq_appetite | DPQ050 | ordinal | PHQ-9 item 5: appetite changes | 0–3 |
| phq_selfworth | DPQ060 | ordinal | PHQ-9 item 6: feeling bad about self | 0–3 |
| phq_concentration | DPQ070 | ordinal | PHQ-9 item 7: concentration difficulty | 0–3 |
| phq_movement | DPQ080 | ordinal | PHQ-9 item 8: psychomotor changes | 0–3 |
| phq_selfharm | DPQ090 | ordinal | PHQ-9 item 9: self-harm thoughts | 0–3 |
| phq_total | Derived | integer | PHQ-9 total score (sum of items 1–9) | 0–27; higher = more depressive symptoms |