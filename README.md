# origin-codegen-model-inorigin

same mission as `origin-codegen-model` (teach an LLM to write Origin code from English instructions) but with a twist that melts my brain a little: the entire fine-tuning pipeline is written *in Origin itself*. LoRA-tuning Qwen3-1.7B via `.or` scripts.

## how it actually works

- `train.or` — drives the `transformer` lib to LoRA-tune Qwen3-1.7B (rank 8 / alpha 16, 5 epochs, seq length 512) on ~84k instruction pairs (`origin_instruction_tuning_dataset_v3.json`)
- `test_model.or` — 10-iteration accuracy eval (`test_set.json`, 20 examples)
- `origin-model.or` — model definition / config side
- REPL included for prompting the trained model interactively

compared to the Python version of this project, the training script here is cleaner and actually coherent — the `.or` wrapper forces a simpler structure, which turns out to be a feature.

## stack

Origin language + JSON datasets, Hugging Face `transformers` + PEFT/LoRA underneath, Qwen3-1.7B. MIT licensed.
