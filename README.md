# LostInSubtitles

Detecting translation errors in English to Hebrew subtitles with LLMs.

Course project, **Large Language Models and Their Applications**, Bar-Ilan University.
Author: Roee Amsalem

> Status: proposal stage. Slides are in [`slides/`](slides/). Code, data and results will be added during the semester.

## Project motivation

Israelis watch most of their TV in English with Hebrew subtitles, so the subtitles carry the meaning.
Bad subtitles are a known problem here. The most famous example: in the series *Rude Awakening*, the line
"I had to chase Christian Slater down the street" was subtitled as "לרדוף אחרי מניח רעפים שהוא נוצרי".
The translator didn't recognize the actor's name and translated it word by word.

Today subtitles are checked by hand, and automatic quality scores only give one number without saying what went wrong.
There is also no labeled English–Hebrew dataset of subtitle errors.

## Problem statement

Given an English subtitle line and its Hebrew translation, decide whether the translation is correct,
and if not, what type of error it contains.

## Input / Output examples

| English | Hebrew subtitle | Label |
|---|---|---|
| I'm not going anywhere | אני לא הולך לשום מקום | Correct |
| You can't miss it | אסור לך לפספס את זה | Meaning error |
| Break a leg | תשבור רגל | Literal idiom |
| Sorry, I didn't mean it, I swear | סליחה | Omission |
| Would you mind closing the door? | סגור את הדלת | Wrong tone |

## Visual abstract

```
OpenSubtitles EN–HE pairs ──► LLM injects one error of a chosen type ──► labeled dataset
                                                                           │
             ┌─────────────────────────────────────────────────────────────┤
             ▼                         ▼                                    ▼
   LLM zero-shot / prompt / few-shot   Fine-tuned multilingual encoder   Small LLM + LoRA
             └──────────────► evaluation: synthetic test set + hand-labeled real test set
```

## Datasets

- **Correct pairs (real):** English–Hebrew aligned subtitle lines from OpenSubtitles (OPUS). Focus on comedies and sitcoms, where idioms and humor are common.
- **Error pairs (synthetic):** generated from correct pairs, see below.
- **Real test set:** ~150 real pairs labeled by hand. Used only for testing, never for training.

Planned size: ~6,000 pairs, half correct and half with errors (~750 per error type).

## Data augmentation and generation

An LLM gets a correct pair and an error type, and rewrites the Hebrew line so it contains exactly that error.
The label is known by construction, so no manual labeling is needed for the training data.
A random sample is reviewed by hand to check that each injected error is real and that there is only one.

## Models and pipelines

| Method | Kind |
|---|---|
| LLM zero-shot (baseline) | Off-the-shelf |
| LLM + system prompt with an error guide | Off-the-shelf |
| LLM few-shot with solved examples | Off-the-shelf |
| Multilingual encoder (e.g. XLM-R) | Fine-tuned |
| Small LLM + LoRA | Fine-tuned |

Specific models: TBD.

## Training process and parameters

TBD (interim report).

## Metrics

- **Detection:** F1 and AUC, correct vs. error
- **Error type:** macro F1 over types, plus a confusion matrix
- **Synthetic to real:** the same metrics on the hand-labeled real set
- **Data quality:** share of injected errors that pass manual review

## Results

TBD.

## Limitations

The model sees one line at a time. Errors that depend on wider context, like the "Hold the door / Hodor" wordplay in *Game of Thrones*,
are out of scope. A possible extension is to add the previous lines of the scene as input.

## Repository structure

```
slides/    proposal, interim and final presentations (PDF/PPTX)
code/      Python scripts and notebooks
data/      datasets (JSON/CSV)
results/   experiment results (CSV/JSON)
visuals/   figures and visual abstract
docs/      project notes, decisions and progress log
```

## Team

Roee Amsalem
