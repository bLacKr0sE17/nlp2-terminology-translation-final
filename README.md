# NLP2 Final Project: Terminology-Aware Machine Translation

This repository contains the notebooks, result files, generated outputs, figures, and final report PDF for an NLP2 final project on sentence-level English--German terminology-aware machine translation.

## Project overview

The project studies terminology-aware machine translation using the WMT25 terminology setup. The goal is to produce fluent German translations while also using required target terms from a terminology dictionary.

The experiments compare prompting-based methods, a random terminology control, lightweight LoRA adaptation, post-processing for chat-style artifacts, model-size diagnostics, candidate selection, terminology repair, and repeated-term consistency diagnostics.

## Main models

- `Qwen/Qwen2.5-1.5B-Instruct`
- `Qwen/Qwen2.5-3B-Instruct`
- Additional small-model diagnostics, including Qwen3 and SmolLM2 variants

## Main metrics

- SacreBLEU for translation quality
- Exact-match terminology accuracy for required term usage
- Boilerplate counts for chat-style artifacts
- Relaxed terminology matching as a diagnostic
- Repeated-term consistency diagnostic

## Repository structure

- `notebooks/`: main experiment notebooks and diagnostic notebooks
- `results/metrics/`: CSV result tables used in the report
- `results/graphs/`: saved figures generated during analysis
- `results/outputs_sample/`: generated output CSV files for reported and diagnostic experiments
- `docs/official_consistency_attempt/`: notes and evidence from the attempted official WMT consistency-script run
- `report/`: final report PDF
- `requirements.txt`: Python package requirements

## Notebooks

- `NLP2_final_project.ipynb`: main Qwen2.5-1.5B prompting, random terminology, initial LoRA, evaluation, and cleanup experiments.
- `NLP2_extra_experiments.ipynb`: Qwen 3B diagnostics, candidate selection, terminology repair, model-family comparison, prompt-format diagnostics, random terminology controls, and repeated-term consistency checks.
- `NLP2_lora_v2_clean_training.ipynb`: clean LoRA v2 adaptation diagnostic.
- `NLP2_lora_training_size_ablation.ipynb`: LoRA v2 training-size ablation.
- `NLP2_official_consistency_check.ipynb`: attempted official WMT consistency-script setup and fallback consistency notes.

## Main findings

Basic terminology prompting improves both BLEU and terminology accuracy over the no-terminology baseline for Qwen2.5-1.5B. Strong prompting increases term adherence but can reduce BLEU for the smaller model.

A Qwen2.5-3B diagnostic shows that a stronger model reduces the quality--adherence tradeoff. The strongest automatic results come from test-time candidate selection and terminology repair, which improves both BLEU and terminology accuracy without additional training.

The random terminology control shows that models may follow supplied terms even when they are incorrect, highlighting the importance of dictionary quality. The initial LoRA setup underperformed prompting-only methods, but cleaner LoRA v2 diagnostics showed that adaptation can help when the instruction data is formatted more carefully.

## Reproducibility notes

The main result tables used in the report are stored in `results/metrics/`, and generated output files are stored in `results/outputs_sample/`.

Some generated output files are raw diagnostic outputs and may contain failure cases such as chat-style boilerplate, multilingual artifacts, or imperfect repair outputs. These files are kept for transparency and error analysis. The report distinguishes these diagnostic outputs from the main evaluated systems.

The original WMT terminology data and trained adapter checkpoints are not redistributed. To rerun the full pipeline, place the WMT terminology data in the expected data folder and run the notebook cells in order.

## Report

The final report PDF is stored in `report/`.
