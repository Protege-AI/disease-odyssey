# Scoring

Each case is asked in two formats, and the two are scored separately. A run is either right or wrong; there is no partial credit.

## Multiple choice

The model sees six options, lettered A through F, and has to answer with exactly one letter ([prompt](../prompts/multiple_choice.txt)). A deterministic parser reads the answer. No model is involved.

The parser accepts a bare letter, a letter with light formatting such as bold or parentheses, and phrasings like "Answer: C" or "The answer is C". It also accepts a letter followed by an explanation. An answer that names two different letters, or that never commits to one, is scored as wrong.

## Free response

The model names the most likely diagnosis in its own words ([prompt](../prompts/free_response.txt)). An LLM judge, GPT-6 Astra, compares the answer with the case's reference diagnosis using the [judge prompt](../prompts/judge.txt) and returns a decision (correct or not) with a short rationale.

The judge gives credit for the same disease under a different name, or for a broader or narrower label that still identifies the same underlying disease. It does not give credit for a different disease, a symptom, an organ system, a risk factor, a complication, or an unranked list of diagnoses.

LLM judges are not perfectly deterministic, so we measure how consistent the judge is:

1. Every free-response answer is judged twice.
2. If the two judgments disagree, the answer is judged 10 more times.
3. The first valid judgment is always the score. The repeats only measure how stable it is, and they never replace it by majority vote.
4. Cases whose judgments still disagree after the repeats are marked as provisional. In the first two releases, this happened for 5 of 3,072 free-response answers.

## Reporting

- Every case is scored. Hard or unanswered cases are not dropped.
- Free-response and multiple-choice accuracy are reported separately.
- Each reported number records the case set, the prompt versions and the judge model behind it.
