# README

## Overview

This artifact contains all materials required to reproduce the experimental results presented in the paper.  
It includes trained SFT and GRPO LoRA models, evaluation datasets, inference pipelines, configuration files, figure-generation scripts, and a pre-computed summary table aggregating IR statistics, latency, instruction counts, and correctness metrics.  
Both full evaluation and lightweight sampling-based evaluation are supported.

---

## Installation

### 1. Download the dataset from Zenodo

Download the dataset package from:

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.17625555.svg)](https://doi.org/10.5281/zenodo.17625555)

After downloading and extracting, place the entire `dataset/` directory directly under the `artifact/` folder:

artifact/

    dataset/
    
        <dataset_files_here>

### 2. Clone this repository

git clone https://github.com/carrotProgrammer/llmveriopt-AE
cd llmveriopt-AE

You should now see:

artifact/
models/
inference/
reproduce_figures/
requirements.txt
README.md

### 3. Install dependencies

Python 3.10+ is recommended.

pip install -r requirements.txt

Main packages: torch, transformers, peft, datasets, pyyaml.

If you need access-controlled models (e.g., Llama family), authenticate first:

huggingface-cli login

---

## Contents

- Trained LoRA adapters (SFT + GRPO variants)
- All evaluation datasets
- Unified inference scripts
- Config files for every model variant
- Scripts to regenerate all figures in the paper
- Author-provided reference outputs
- A complete summary table used to generate plots

---

## Directory Structure

artifact/
    models/
    dataset/
    inference/
        run_inference_demo.sh
        run_inference_all.sh
        run_model_latency.sh
        configs/*.yaml
    reproduce_figures/
        summary_table/
        reproduce_figures.sh
    README.md

---

## Quick Start

### Sampling-based evaluation (recommended)

cd inference
chmod +x run_inference_demo.sh
./run_inference_demo.sh

This runs a small subset of the test data and completes within minutes on common GPUs.

### Full evaluation (large GPU required)

cd inference
chmod +x run_inference_all.sh
./run_inference_all.sh

Running all models across the entire test set requires ≥ 32GB GPU memory.  
Devices with less memory may encounter OOM failures.

### Final model evaluation (model_latency)

cd inference
chmod +x run_model_latency.sh
./run_model_latency.sh

This script reproduces the full evaluation for the primary model used in the paper.

---

## Reproducing Figures

All plots in the paper can be regenerated using:

cd reproduce_figures
chmod +x reproduce_figures.sh
./reproduce_figures.sh

The script reads the included summary table and writes all outputs to:

reproduce_figures/outputs/

---

## Expected Outputs

Running inference scripts produces:

inference/output/<model_name>/results.csv

The figure-generation script reproduces all plots and tables from the paper.

---

## Notes for Evaluators

- Linux OS is recommended.
- Insufficient GPU memory will result in out-of-memory errors.
- All decoding is greedy → deterministic outputs.
- CPU-only execution is functional but extremely slow.

