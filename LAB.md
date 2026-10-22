# ITOM-6229 Lab: Compare CoT, Act-only, and ReAct

Suggested duration: 75–90 minutes. Work individually or with a partner as directed by your instructor. Each student should save work in their own repository unless a shared team repository is assigned.

## Learning objectives

By the end of this lab, you should be able to trace an agent's actions and observations, compare reasoning without tools, tools without explicit reasoning text, and their combination, identify a failure, and describe a business use with appropriate controls.

## Before class — instructor preparation

Provide a working assignment repository, an approved Responses API model ID, and API access. Test one live run before class. Codespaces and model API usage have separate costs. This lab uses a modernized teaching notebook rather than reproducing the paper's benchmarks. Use the same model ID for all methods.

## Part 1 — Launch and inspect (15 minutes)


1. Open your individual assignment repository from [Classroom50](https://classroom50.org/ITOM-6229/agentic-ai/assignments). If a repository has not been created for you, follow the instructor's template-copy instructions.
2. Before starting, add `OPENAI_API_KEY` under your GitHub account **Settings → Codespaces → New secret**, granting access to your individual repository. Use your own or an individually issued course API key.
3. Select **Code → Codespaces → Create codespace** in your repository. Python 3.11, Python/Jupyter extensions, and packages install automatically. Wait for setup to finish.
4. Open `hotpotqa_classroom.ipynb`. Select **Python 3 (ReAct)** as its kernel. In the setup cell, enter the instructor-approved model ID in `OPENAI_MODEL`, or configure that environment variable and restart the codespace.
5. Run the setup and method-definition cells, then pause before the experiment cell for Part 2. All three methods use question IDs **0, 1, and 2** from the bundled HotpotQA development data. Do not run the original 500-question experiment.
6. Inspect outputs and `results/hotpotqa_results.json`. Begin `LAB_NOTES.md`.

The instructor must supply an approved Responses API model ID and API access before live execution. The notebook uses [the OpenAI Responses API](https://developers.openai.com/api/docs/guides/text?lang=python). A GitHub token does not provide model API access. API calls incur separate usage charges; Codespaces usage depends on your account or course organization allowance. Stop your codespace when finished.

Each question uses one CoT request and up to seven requests each for Act-only and ReAct: at most 15 model requests per question, or 45 for the initial lab run. Both agents use the same seven-step limit, without extra formatting-recovery model calls. A malformed action consumes a step. Reruns incur additional usage; request counts and elapsed time are not dollar-cost estimates.

Checkpoint: Show your partner or instructor the Python kernel and locate the model ID, allowed actions, and seven-step limit. Do not display your API key.

## Methods being compared

| Method | Explicit explanation/rationale | Wikipedia tools | Upstream prompt key |
|---|---|---|---|
| CoT | Brief explanation followed by answer | No | `cotqa_simple6` |
| Act-only | No requested Thought text | Search, Lookup, Finish | `webact_simple6` |
| ReAct | Brief rationale before each action | Search, Lookup, Finish | `webthink_simple6` |

The prompt sets contain the same six demonstration questions. CoT uses one response per test question; Act and ReAct can interact with the environment for seven steps. The same model and per-response output cap are used, but total token budgets and runtimes differ. Act-only omits explicit reasoning text; it does not disable internal model reasoning. This lab requests concise explanations and rationales rather than reproducing the original reasoning traces. It uses single-run CoT, not self-consistency voting.

## Part 2 — Predict the behavior (10 minutes)

Before running the experiment cell, inspect the first three questions in the bundled data. Predict an outcome for each method. In LAB_NOTES.md, predict which questions could benefit from search. Locate Search, Lookup, and Finish in the code and explain what each does. Identify where an observation is added to the next model prompt.

## Part 3 — Run and compare (20 minutes)

Run the experiment cell once for IDs 0, 1, and 2. Read the saved results and fill in the comparison table in LAB_NOTES.md: all three answers, ground truth, exact-match scores, model calls, tool calls, status, and elapsed time. Keep the same model for all three methods.

Checkpoint: Compare Act-only and ReAct on one question: show an action, its observation, and the following action or final answer. Contrast both with the CoT explanation and answer. Discuss whether the final answer is supported by retrieved evidence. If execution fails, record the error and ask the instructor for help; do not repeatedly rerun a failing API call.

## Part 4 — Diagnose and propose an improvement (15 minutes)

Identify a wrong answer, invalid format, unhelpful search, or fragile assumption. If all examples succeed, choose a plausible failure grounded in the code. Write a specific improvement and a test that could detect whether it helps. Explain why three examples cannot establish that one method is generally better. Discuss whether search helped, whether a rationale improved action selection, and whether extra calls were worthwhile.

Optional extension, if time and the instructor's API budget permit: make one change to the prompt or step limit, preserve the original results, and rerun only one question in a separate cell. Record the exact change and the new outcome separately.

## Part 5 — Discuss a business application (10 minutes)

Describe one business task that could use this pattern. Name its tools, one action requiring human approval, and one measurable success criterion. Discuss whether a correct answer is enough to count the business task as completed.

## Wrap-up and lab check-off (5–10 minutes)

Commit and push the following to your individual or assigned team repository:

- `hotpotqa_classroom.ipynb` with executed outputs.
- `results/hotpotqa_results.json` with nine method/question records and their traces (or saved partial results if execution failed).
- `LAB_NOTES.md` with your name, model ID, predictions for all three methods, comparison table, evidence, failure analysis, and business application.

If execution is incomplete, preserve partial results and explain the error in your notes. Show your instructor the pushed files and submit the repository URL through Classroom50 if requested. Deadlines and credit follow the instructor's lab announcement.

Stop your codespace when finished. Keep keys and tokens in Codespaces secrets, never in notebook outputs or submitted files.

## Historical models and software

The [ReAct paper](https://arxiv.org/pdf/2210.03629) uses PaLM-540B for its main prompting experiments, PaLM-8B/62B for fine-tuning studies, and GPT-3 `text-davinci-002` with greedy decoding in Appendix A.1.

The [original HotpotQA notebook](https://github.com/ysymyth/ReAct/blob/master/hotpotqa.ipynb) records Python 3.7.4 in its metadata and calls `openai.Completion.create` with `text-davinci-002` and temperature 0. Notebook metadata is not a complete specification of the paper's runtime. The upstream README does not pin exact package versions.

This lab configures Python 3.11 and the dependencies in requirements.txt. These are teaching-environment choices, not versions reported by the paper. Record the actual model and installed versions used in your session.

## Troubleshooting

The notebook runs in the VS Code Jupyter extension with `ipykernel`; a full JupyterLab server is not installed. The remaining packages support model calls, Wikipedia retrieval, and the original environment/wrappers.

If Codespaces setup stalls, select **View logs**. Look for `Installing minimal lab dependencies...` to see whether package setup has started. If logs stop before that message, dependency installation has not yet begun. After updating the repository, rebuild an existing Codespace to apply the configuration.


- **Packages missing:** In the repository-root terminal, run `python -m pip install -r requirements.txt`, then restart the notebook kernel.
- **Missing key/model:** Add the Codespaces secret and restart the codespace; supply the instructor-approved model ID. Do not print secret values.
- **Authentication, quota, or model-access error:** Check access with the instructor before repeating runs.
- **Wikipedia error/empty observation:** The upstream environment scrapes live Wikipedia; markup and access restrictions can change. Record the error, retry later, and explain incomplete execution in your report. Do not fabricate results.
- **Execution interrupted:** Results are saved after each method/question run. Preserve the existing file before rerunning; the experiment cell starts a new run.
- **Original notebooks fail:** They retain historical APIs and models. The dependency setup targets the classroom notebook. ALFWorld and WebShop need separate environment/data setup.
