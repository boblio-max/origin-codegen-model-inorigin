# origin-codegen-model-inorigin

A code generation model that translates natural language instructions into [Origin](https://github.com/origin-lang/origin) code. Built on Qwen3-1.7B with LoRA fine-tuning.

## Overview

This project fine-tunes a small language model to generate Origin programs from plain English descriptions. The training dataset contains ~84k instruction-output pairs covering arithmetic, loops, conditionals, lists, and more.

## Repository Contents

| File | Description |
|------|-------------|
| `origin_instruction_tuning_dataset_v3.json` | Training dataset (~84k samples) |
| `test_set.json` | Evaluation dataset (20 examples with expected outputs) |
| `train.or` | Training script (Origin + transformer module) |
| `test_model.or` | Accuracy evaluation script |
| `origin-model.or` | Interactive inference REPL |

## Requirements

- Origin language runtime
- Python packages: `transformers`, `peft`, `datasets`

## Usage

### Train the model

```bash
origin train.or
```

This will:
1. Load the Qwen3-1.7B base model
2. Apply LoRA adapters (r=8, alpha=16, targets: q_proj/v_proj)
3. Train for 5 epochs with batch size 2 and learning rate 2e-4
4. Save the fine-tuned model to `./origin_codegen_model`

### Evaluate accuracy

```bash
origin test_model.or
```

Runs 10 iterations of shuffled test examples and reports average accuracy.

### Interactive inference

```bash
origin origin-model.or
```

Opens a REPL where you type natural language instructions and the model generates Origin code.

## Training Configuration

- **Base model:** Qwen/Qwen3-1.7B
- **Method:** LoRA (rank 8, alpha 16)
- **Target modules:** q_proj, v_proj
- **Max sequence length:** 512
- **Batch size:** 2
- **Epochs:** 5
- **Learning rate:** 2e-4
- **Gradient accumulation:** 2

## License

MIT
