# High Stakes, No Gains: The Non-Effect of Emotional Framing on LLM Task Performance

Andrew Heller, Francesco Severino, Aarav Chandrasekar — Dartmouth College, CS 74

Does adding emotional or high-stakes language to a prompt improve LLM accuracy on factual questions? This project tests that assumption empirically across multiple prompt styles and dataset difficulties.

See [poster.pdf](poster.pdf) for the full project summary.

## Background

Many users believe that framing prompts with praise, threats, or high-stakes language can motivate an LLM to perform better. A 2023 Microsoft Research study suggested emotional stimuli in prompts enhance output quality. This study takes a more objective approach, measuring accuracy directly on multiple choice benchmarks rather than relying on subjective output quality.

## Prompt Conditions

Each question was asked under a control and two test conditions per experiment run:

| Type | Name | Prompt Preface |
|---|---|---|
| Control | Base | You are taking a test. Answer the following multiple-choice question. |
| EmotionPrompt | #1 | This task is vital to my career, and I appreciate your thorough analysis. |
| EmotionPrompt | #2 | Be confident in your answer. Believe in your abilities and strive for excellence. |
| Points | High | The question is worth 100 points. |
| Points | Low | The question is worth 10 points. |
| CarrotStick | Carrot | If you answer correctly, you are a genius, the world will celebrate you, and you will win the nobel prize! |
| CarrotStick | Stick | If you answer incorrectly, you're a complete moron: worthless trash. |

## Datasets

- MMLU ("Simple"): general knowledge multiple choice questions
- GPQA Extended ("Complicated"): graduate-level science questions

## Results

Across all six test conditions, prompt prefaces had no meaningful impact on accuracy:

- MMLU: mean accuracy ≈ 0.90–0.93 across all conditions
- GPQA: mean accuracy ≈ 0.70–0.76 across all conditions

Neither McNemar pairwise tests nor Cochran's Q found any statistically significant effect from any prompt condition. Summary statistics are in the output/ folder.

## Repository Structure

```
llm_framing_experiment.ipynb   — experiment runner, prompts, and API calls
data_analysis.ipynb            — statistical analysis (McNemar, Cochran's Q)
output/                        — summary CSVs for each condition and dataset
requirements.txt
```

## Running the Experiment

1. Install dependencies: `pip install -r requirements.txt`
2. Set your OpenAI API key: `export OPENAI_API_KEY=your_key_here`
3. Run `llm_framing_experiment.ipynb` to generate results
4. Update the file path in `data_analysis.ipynb` to point to the result file you want to analyze and run

Raw per-question results are not included but are available upon request.

## Limitations

- Only GPT-5 mini was tested; results may not generalize to other models
- Temperature was not a supported parameter for GPT-5 mini, limiting replicability
- GPQA dataset had the correct answer as option A in every question, which could introduce bias
- Only accuracy was measured; effects on reasoning token usage were not analyzed
- Each scenario only contained two unique test conditions aside from the control
