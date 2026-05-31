# CSE 151B Competition — Final Submission

**Model:** Qwen3-4B-Thinking-2507 + Round 1 QLoRA adapter (`a3jiang/qwen3-4b-sft-round1`)

## Hardware & Timing

| | |
|---|---|
| GPU | 2× NVIDIA T4 (16 GB each) |
| Total inference time | ~50–60 hours (full private set) |

## Model Weights

No manual download needed. The base model and adapter load automatically from HuggingFace Hub:

| Component | Hub path |
|---|---|
| Base model | `Qwen/Qwen3-4B-Thinking-2507` |
| QLoRA adapter | `a3jiang/qwen3-4b-sft-round1` |

## Kaggle Setup

The notebook runs on Kaggle. Attach the public dataset **`alanj21/dataset1`** as an input
(it will be mounted at `/kaggle/input/datasets/alanj21/dataset1`). It must contain:

| File | Purpose |
|---|---|
| `judger.py` | scoring logic |
| `utils.py` | utilities |
| `private2.jsonl` | private test questions |
| `checkpoint_private.jsonl` | pre-computed checkpoint (skips completed questions) |

No other datasets need to be attached.

## Running Inference

Open `run_inference.ipynb` on Kaggle and run all cells top to bottom. The final cell calls:

```python
results = run_inference()
```

This will:
1. Load `Qwen3-4B-Thinking-2507` (4-bit quantized) + the Round 1 QLoRA adapter from HuggingFace Hub
2. Resume from the pre-computed checkpoint — already-completed questions are skipped automatically
3. Append remaining generations to `/kaggle/working/checkpoint_private.jsonl`
4. Write the final submission CSV to `/kaggle/working/submission.csv`

All hyperparameters are set to the final submission values — no configuration changes needed.

## Repository Contents

| File | Description |
|---|---|
| `run_inference.ipynb` | Main entry point — run this on Kaggle |
| `judger.py` | Response scoring logic |
| `utils.py` | Utilities used by `judger.py` |
