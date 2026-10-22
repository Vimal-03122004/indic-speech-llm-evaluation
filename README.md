# Indic Speech LLM Evaluation (Tamil + English)

**Prepared by:** Vimal D

## Overview
Offline speech-to-text-to-LLM evaluation using Whisper-small for ASR and Qwen2.5-0.5B-Instruct for text response generation. Dataset: 100 Google FLEURS test examples, 50 Tamil (`ta_in`) and 50 English (`en_us`).

## Contents
- `report.pdf` — full report with measured results and an exploratory response-quality review.
- `notebooks/Untitled7.ipynb` — supplied Colab notebook.
- `results/asr_results.csv` — 100 per-example clean-audio ASR results.
- `results/asr_metrics.csv` — WER/CER/latency/RTF summary.
- `results/noisy_asr_results.csv` — noisy-audio ASR predictions.
- `results/noise_comparison.csv` — clean versus synthetic-noise metrics.
- `results/pipeline_results.csv` — 100 transcripts, generated LLM responses, and latency.
- `results/pipeline_latency_summary.csv` — average latency by language.
- `results/response_quality_audit.csv` — exploratory qualitative review of the first 10 outputs per language.

## Main results
- Tamil WER: 0.7334 beam search (`num_beams=5`) vs 1.1134 greedy (`num_beams=1`).
- English WER: 0.2507 beam search vs 0.2545 greedy.
- At 15 dB synthetic Gaussian noise, Tamil WER rises from 0.7334 to 0.8010; English WER rises from 0.2507 to 0.2817.
- Mean end-to-end latency: English 2.631 seconds; Tamil 5.778 seconds.

## Response-quality review
An exploratory, assistant-assisted qualitative review inspected the first 10 LLM outputs per language. It is subjective, small, and not a blinded expert annotation. The report therefore treats it as diagnostic evidence, not a benchmark-quality hallucination rate. The audit flags examples with unclear/incomplete responses or unsupported/inaccurate additions. A stronger follow-up should use independent annotators and a purpose-built spoken QA dataset with verified expected answers.

## Reproducibility
1. Open `notebooks/Untitled7.ipynb` in Google Colab and enable GPU runtime.
2. Run cells in order; internet is required for model and dataset downloads.
3. The CSVs in `results/` contain the supplied run's captured outputs.
4. Library versions, GPU availability, and runtime behavior can change across sessions.

## Limitations
- 50 samples per language; read speech, not conversational QA.
- Synthetic Gaussian noise rather than real-world environmental recordings.
- Offline sequential latency; no time-to-first-token or full-duplex streaming measurement.
- The beam-search comparison is a decoding experiment, not a new architecture.
- Streaming improvement is proposed future work, not implemented.
- The qualitative response review is exploratory and should not be generalized to all 100 responses.

## References
1. Xu et al. (2025), *Qwen2.5-Omni Technical Report*. https://arxiv.org/abs/2503.20215
2. Défossez et al. (2024), *Moshi: a speech-text foundation model for real-time dialogue*. https://arxiv.org/abs/2410.00037
3. Radford et al. (2022), *Robust Speech Recognition via Large-Scale Weak Supervision*. https://arxiv.org/abs/2212.04356
4. Google FLEURS dataset: https://huggingface.co/datasets/google/fleurs
5. Qwen2.5-0.5B-Instruct model card: https://huggingface.co/Qwen/Qwen2.5-0.5B-Instruct
