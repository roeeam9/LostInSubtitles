# Project Overview

Final project for the course **Large Language Models and Their Applications**, Bar-Ilan University.
Author: Roee Amsalem (solo project).

## Course requirements
- Solve a novel, relevant task using LLMs / GenAI.
- Recommended approach: a task with no existing dataset, so synthetic data is generated for training and evaluation.
- Compare several methods: fine-tuned models vs. off-the-shelf models.
- Milestones: proposal (week 5), interim report (week 9), final report (week 13), GitHub submission two weeks after the semester.

## Problem
Hebrew subtitles of English shows often contain translation errors: wrong meaning, idioms translated word by word,
missing parts, wrong tone, names translated as words. There is no labeled dataset of such errors in Hebrew.

## Task
Input: an English subtitle line and its Hebrew subtitle.
Output: `correct`, or one error type: `meaning_error`, `literal_idiom`, `omission`, `wrong_tone`.

## Data
- Correct pairs from OpenSubtitles (OPUS), English–Hebrew.
- Error pairs: an LLM injects one error of a given type into a correct pair. Label known by construction.
- Real test set: ~150 real pairs labeled by hand.

## Methods to compare
1. LLM zero-shot (baseline)
2. LLM + system prompt
3. LLM few-shot
4. Fine-tuned multilingual encoder (e.g. XLM-R)
5. Small LLM + LoRA

## Research questions
- Does a small fine-tuned model beat a large prompted model on this task?
- Which error types are hardest to detect?
- Do models trained on injected errors catch real ones?
