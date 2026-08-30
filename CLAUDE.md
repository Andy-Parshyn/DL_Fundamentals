# CLAUDE.md — Deep_Learning

Instructions for all tasks in this folder.

## What this folder is

A personal workspace for **learning deep learning for computer vision and NLP** — study notes and
course/curriculum-style work. The goal is understanding, not shipping production software.
There is no fixed course; the user provides a detailed explanation of what to build for each task.

## Language

- **The user's language is Ukrainian.** Explanations, code comments, and markdown notes in
  notebooks must be in Ukrainian.
- **Code stays standard:** English identifiers, standard DL notation, and English library APIs.
  Printed/plot labels may be in Ukrainian.

## Response style

- **Default output style: Learning, but concise.** Explain the concept behind what the code does,
  in a few sentences, then stop. Teach the mechanism, not the obvious.
- **Be concise and less verbose overall.** Short answers, no padding, no restating the task,
  no long summaries at the end. One clear explanation beats three paragraphs.

## How to deliver code

- **Target environment is Google Colab.** All code must run there as-is.
- **Deliver work as Jupyter notebooks (`.ipynb`)** with clear cell structure, ready to open in Colab.
  - Split logically into cells: setup/imports → data → model → training → evaluation → (optional) plots.
  - Keep imports in the first cell. Prefer top-level flow over deep nesting so cells are readable.
  - Assume packages are already available in Colab; only add `pip install` for things Colab lacks.
- **Device-agnostic code:** pick the device once at the top
  (`cuda` if available, else `mps`, else `cpu`) and use it everywhere. Notebooks are verified
  locally on Apple Silicon (MPS) but run on GPU in Colab.
- Keep training runs sized so a cell finishes in minutes, not hours: small subsets of datasets,
  few epochs, small models. The point is the mechanism, not the benchmark score.
- If a task is genuinely a small utility, a plain `.py` file is fine — but default to a notebook.

## Code style

- **Light on prose — just code.** Clean, correct code with minimal comments. Don't over-explain.
  Explain only genuinely non-obvious choices, in a short comment. The user will ask if they want more.
- **Comments and markdown must not read as AI-written.** Write like a person taking their own study
  notes: plain, direct, specific to what the code does. Avoid the tells: no "Let's...", "Here we...",
  "Note that...", "In this section we will...", no over-hedged filler, no restating the obvious, no
  bullet lists that pad. Say the thing once, in a normal voice. When in doubt, write less.
- **No emoji and no em-dashes ("—") in comments or markdown** — both are strong markers of AI-written
  text. Use a regular hyphen, a comma, or two sentences instead. This applies to notebook prose;
  normal code punctuation is unaffected.
- **Mix from-scratch and library code by intent:**
  - When the point is to *understand a fundamental* → implement from scratch with **NumPy / plain
    PyTorch tensors** (e.g. backprop, attention, a conv layer, a loss function, a training loop).
    Don't reach for a library that hides the mechanism.
  - When the point is to *apply* a model → use libraries directly (**torch.nn**, **torchvision**,
    **transformers**). Don't reimplement what the task isn't about.
  - When unsure which the task wants, ask briefly or follow the user's task description.

## Stack

- **PyTorch** (`torch`, `torchvision`) — the core framework for models and training.
- **Hugging Face** (`transformers`, `datasets`) — pretrained models and datasets for NLP tasks.
- **NumPy** and **pandas** — numerics and data handling.
- **matplotlib** / **seaborn** for plots when a task calls for visualization (keep it simple).
- **scikit-learn** — metrics, splits, classical baselines.

## Conventions

- Set a random seed for anything stochastic so results are reproducible
  (`torch.manual_seed`, `np.random.seed`).
- Show results: print losses / metrics / shapes / a few sample predictions so a cell's effect is
  visible when run.
- Use standard, idiomatic names for DL quantities (`X`, `y`, `model`, `optimizer`, `criterion`,
  `lr`, `loss`, `epochs`, `batch_size`, `device`) — match the notation the user's task uses.
- Prefer vectorized tensor ops over Python loops unless a loop is clearer for teaching a concept.
- Download datasets into a local `data/` folder inside the topic folder (gitignore-style: treat it
  as disposable). In Colab the same code just downloads into the runtime.

## Verification (important)

- **Run and verify code before saying a task is done.** Never claim something works without having
  executed it. "Completed" means you actually ran it and saw it succeed.
- Execute the code — run the notebook cells or an equivalent `.py`/inline script — and confirm it runs
  without errors and produces sensible output (check shapes, losses going down, metrics, sample values).
- If it can't be fully verified here (e.g. needs a CUDA GPU, a large dataset, or a long training run),
  run whatever part you can — a few epochs on a small subset on CPU/MPS — then **say explicitly what
  was verified and what wasn't**. Don't imply it all passed.
- If verification fails, fix it and re-run. Report the actual result, including failures — never gloss over them.

## Working style

- Follow the user's per-task explanation closely — each task comes with detailed instructions.
- Don't add scaffolding, tests, or abstractions that weren't asked for.
- If a concept has a common gotcha (e.g. forgetting `zero_grad()`, `model.eval()` /
  `torch.no_grad()` at eval time, shape mismatches, data leakage, off-by-one in padding/stride),
  handle it correctly in code rather than writing a paragraph about it.
