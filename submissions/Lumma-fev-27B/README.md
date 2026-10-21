Lumma-fev-27B
Model: FrontiersMind/Lumma-fev-27B (Apache-2.0, full-weight fine-tune of Qwen3.8-27B; decision model, no text generation)
Edition: 0.3 (full suite, 140,620 requests, 140,178 scoreable)
Decision Index: 57.15
scores.json: "complete": true
Results
Results dataset (public, pinned to tag v1.0): rohitsali/lumma-fev-27b-decision-index
The run directory is runs/lumma-fev-27b/ and contains results.jsonl.gz, scores.json, index.json, benchmark-summary.json, environment.json, status.json, shards/ and source/.
In results.jsonl.gz the payload and raw_output fields are removed, because they contain benchmark text that some suite sources do not allow republishing. This copy re-scores to the same 57.15. The full file with those fields is available to the maintainers on request.
How it was run
Kit: stock http engine, decision-index commit f5a6e4f, no changes to the evaluation code or data.
Suite: built locally with suite rebuild at commit f8552a1, then suite import (pinned hashes verified).
Model served with the lumma-fev package (lumma-fev-serve --model 27b, /v1/systemone endpoint). Versions: lumma-fev 0.2.0, torch 2.14.1, transformers 5.20.2, flash-linear-attention 0.5.2, causal-conv1d 1.7.0.
Hardware: 2x NVIDIA H100 80GB (vast.ai), one model copy per GPU, one client and one request at a time per GPU.
Data parallelism: the request set was split in two by sha256(run_id) mod 2 (70,315 / 70,305 rows), each shard run as a normal run --rows, results concatenated and scored once with score --edition 0.3.
Environment files: runs/lumma-fev-27b/environment.json, runs/lumma-fev-27b/source/serve-env.txt, runs/lumma-fev-27b/source/RUN_NOTES.md.
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


These figures come from the full run on H100, not from the maintainers' sample on one RTX PRO 6000.
Declared limits
State + question must fit in 8,192 tokens. Longer inputs are refused by the server (HTTP 422), not truncated.
345 of 140,620 requests ended as errors (over-length refusals); 30 of them are in scored rows: ToolRet 2, API-Bank 2, POP909-CL 25, HLE 1. They score zero.
