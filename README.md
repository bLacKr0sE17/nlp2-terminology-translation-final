# NLP2 Final Project: Terminology-Aware Machine Translation

This repository contains the notebooks, result files, and report for an NLP2 final project on sentence-level English--German terminology-aware machine translation.

## Project overview

The project studies terminology-aware machine translation using the WMT terminology setup. The goal is to produce fluent German translations while also using required target terms from a terminology dictionary.

We compare prompting-based methods, a random terminology control, lightweight LoRA adaptation, post-processing for chat-style artifacts, model-size diagnostics, candidate selection, terminology repair, and repeated-term consistency diagnostics.

## Main models

- Qwen/Qwen2.5-1.5B-Instruct
- Qwen/Qwen2.5-3B-Instruct
- Additional small-model diagnostics, including Qwen3 and SmolLM2 variants

## Main metrics

- SacreBLEU for translation quality
- Exact-match terminology accuracy for required term usage
- Boilerplate counts for chat-style artifacts
- Relaxed terminology matching as a diagnostic
- Repeated-term consistency diagnostic

## Repository structure

- notebooks/: contains the main and extra experiment notebooks
- report/: contains the final ACL-style report source and PDF
- results/metrics/: contains CSV result tables
- results/graphs/: contains saved figures
- results/outputs_sample/: contains generated output CSV files
- scripts/: optional helper scripts
- docs/: additional notes

## Notebooks

The main experimental workflow is provided in notebooks/NLP2_final_project.ipynb.

Additional diagnostics, including Qwen 3B model-size experiments, candidate selection, terminology repair, repeated-term consistency, random terminology controls, and model-family comparisons, are provided in notebooks/NLP2_extra_experiments.ipynb.

## Main findings

Basic terminology prompting improves both BLEU and terminology accuracy over the no-terminology baseline for Qwen2.5-1.5B. Strong prompting increases term adherence but can reduce BLEU for the smaller model.

A Qwen2.5-3B diagnostic shows that a stronger model reduces the quality--adherence tradeoff. The strongest automatic results come from a test-time candidate selection and terminology repair strategy, which improves both BLEU and terminology accuracy without additional training.

The random terminology control shows that models may follow supplied terms even when they are incorrect, highlighting the importance of dictionary quality. Lightweight LoRA adaptation underperformed prompting-only methods, but test-time repair partially improved cleaned LoRA outputs.

## Reproducibility

The main result tables used in the report are stored in results/metrics/, and key figures are stored in results/graphs/.

The original WMT terminology data is not redistributed here unless allowed by the course/project instructions. To rerun the full pipeline, place the WMT terminology data in the expected data folder and run the notebook cells in order.

## Report

The final ACL-style report source and PDF are stored in report/.
