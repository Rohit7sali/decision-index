Lumma-fev-27B
Model: FrontiersMind/Lumma-fev-27B (Apache-2.0, full-weight fine-tune of Qwen3.8-27B; decision model, no text generation)
Edition: 0.3 (full suite, 140,620 requests, 140,178 scoreable)
Decision Index: 57.15
scores.json: "complete": true
Results
Full results (compact copy, without payload / raw_output; re-scores to the same 57.15): https://huggingface.co/datasets/rohitsali/decision-index-results/tree/main/runs/lumma-fev-27b-compact
Full results (with payload): same dataset, runs/lumma-fev-27b/
The results dataset is private because results.jsonl contains benchmark text in the payload field, which some suite sources do not allow us to republish. See the PR description for access.
How it was run
Kit: stock http engine, decision-index commit f5a6e4f, no changes to the evaluation code or data.
Suite: built locally with suite rebuild at commit f8552a1, then suite import (pinned hashes verified).
Model served with the lumma-fev package (lumma-fev-serve --model 27b, /v1/systemone endpoint). Versions: lumma-fev 0.2.0, torch 2.14.1, transformers 5.20.2, flash-linear-attention 0.5.2, causal-conv1d 1.7.0.
Hardware: 2x NVIDIA H100 80GB (vast.ai), one model copy per GPU, one client and one request at a time per GPU.
Data parallelism: the request set was split in two by sha256(run_id) mod 2 (70,315 / 70,305 rows), each shard run as a normal run --rows, results concatenated and scored once with score --edition 0.3.
Environment files: runs/lumma-fev-27b/environment.json, source/serve-env.txt, source/RUN_NOTES.md.
Latency
Measured on H100 80GB, one request at a time per GPU, over ok rows of the full run:

median
mean
p80
p95
105.8 ms
335.7 ms
284.0 ms
1280.9 ms


These are from the full run, not the maintainers' private sample on one RTX PRO 6000, which should be measured separately.
Declared limits
State + question must fit in 8,192 tokens. Longer inputs are refused by the server (HTTP 422), not truncated.
345 of 140,620 requests ended as errors (these over-length refusals); 30 of them are in scored rows: ToolRet 2, API-Bank 2, POP909-CL 25, HLE 1. They score zero.
