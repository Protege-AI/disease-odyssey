# Disease Odyssey

Prompts for Disease Odyssey, a benchmark from Protege DataLab that tests whether a model can name a serious condition from a real patient's record before it was diagnosed.

Each case is one patient's de-identified record, cut off at the first day a serious diagnosis was documented. That day and everything after it are removed, and a lab result is kept only if both its specimen and its result were dated before the cutoff. The model reads the remaining record and names the single new, serious condition that is developing. The diagnosis documented after the cutoff is the reference answer.

The first two releases have 256 physician-accepted cases across 129 ICD-10 categories. The blog post describes how cases are built, checked and reviewed, and reports results for four frontier models.

## What's in this repository

| File | What it is |
|---|---|
| [`prompts/free_response.txt`](prompts/free_response.txt) | Task prompt for free response: the model names the diagnosis in its own words |
| [`prompts/multiple_choice.txt`](prompts/multiple_choice.txt) | Task prompt for multiple choice: the model picks one of six lettered options |
| [`prompts/judge.txt`](prompts/judge.txt) | Prompt for the LLM judge that grades free-response answers |
| [`docs/scoring.md`](docs/scoring.md) | How both formats are scored, including the judge consistency protocol |

The prompts are the exact versions used for the results in the blog post.

## Placeholders

- `{{ patient_record }}` (both task prompts): the case's record before the cutoff, as plain text.
- `{{ options }}` (multiple choice): six options, one per line, written as `A. <diagnosis>` through `F. <diagnosis>`. One is the reference diagnosis and five are plausible alternatives.
- `{reference_answer}` and `{model_answer}` (judge): the case's reference diagnosis and the model's free-response answer.

## What's not included

The cases are built from de-identified patient records and are handled as sensitive health data, so they are not public. That includes the records, the reference diagnoses, the multiple-choice options, physician reviews and model outputs. The benchmark is for evaluation only, not for training or fine-tuning.

## License

The contents of this repository are licensed under [CC BY 4.0](LICENSE).
