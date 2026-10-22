# ITOM-6229 Lab notes: CoT, Act-only, and ReAct

Name / partner (if applicable):

Model ID:

Repository URL:

## Part 1: Environment and agent components

Python version:

Installed package versions (run `python -m pip freeze` in the terminal):

Model output-token cap and tool-step limit:

## Part 2: Predictions

Predict which method will work best for each question and explain why. Identify the prompt key, tools, and stopping condition for each method.

## Part 3: Results

Copy the actual answers, scores, and metrics from the saved JSON; record errors as unscored.

| Question ID | Method | Answer | Ground truth | EM | Model calls | Tool calls | Seconds | Status |
|---|---|---|---|---|---|---|---|---|
| 0 | CoT | | | | | | | |
| 0 | Act-only | | | | | | | |
| 0 | ReAct | | | | | | | |
| 1 | CoT | | | | | | | |
| 1 | Act-only | | | | | | | |
| 1 | ReAct | | | | | | | |
| 2 | CoT | | | | | | | |
| 2 | Act-only | | | | | | | |
| 2 | ReAct | | | | | | | |

## Part 3: Evidence from the three methods

For one question, compare the CoT answer/explanation with Act-only and ReAct action/observation traces. Did search help? Did an explicit rationale help select an action? Cite evidence rather than assuming a method must win.

## Part 4: Failure analysis and proposed improvement

Discuss correctness, extra calls, a specific failure or fragile assumption, an improvement, and a test. What remains uncontrolled? Why can this sample not establish general superiority?

## Part 5: Business application and controls

## Execution issues and partial results (if any)
