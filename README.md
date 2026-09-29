# DASE7506 MP1 - Small Language Model Challenge

Full-test CPU FP32 BPB: **1.7228267184138215**.

## Files

- **MP1_Code.zip**: complete executable code, fixed benchmark data/tokenizer, six-page report, exact install/train/evaluate instructions, nine-run experimental evidence, and integrity manifests.
- **report.pdf**: six-page report, also included inside the code archive.
- The matching **MP1_Checkpoints.zip** is published as a repository Release attachment. It contains the final checkpoint and the separate original baseline checkpoint for timing only.

Download MP1_Code.zip and MP1_Checkpoints.zip. Extract both into the same parent directory to obtain `mp1-code/` and `mp1-checkpoints/`. Follow `mp1-code/README.md` for complete installation and reproduction. No retraining is required to score the final predictor.

```bash
cd mp1-code
python3.12 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python scripts/verify_release.py
python evaluate.py --checkpoint ../mp1-checkpoints/checkpoint.pt --device cpu --precision fp32 --threads 4 --split test --output reproduced/final-test.json
```

The final model has width 192, depth 4, heads 4, context 256, vocabulary 2048 and dropout 0. It was trained from scratch with seed 42 for 3,600 updates, batch 32 (29,491,200 targets), and selected on validation before testing. Checkpoint SHA-256:

`84cdce4e8b8b99169e5a9b5a1010aad3221865bf1693e154e15314c00d71a0dc`

Original measured scoring ratio: 1.229x baseline; peak process RSS: 2.117 GiB; final checkpoint: 8.494 MiB. Full evidence and limitations are included. The report distinguishes the combined training/width test improvement from the equal-target width ablation. No novel architecture is claimed.

## AI assistance and attribution

Substantive OpenAI Codex assistance was used for assignment interpretation, environment troubleshooting, experiment design, residual-dropout implementation, run commands, result analysis, report preparation, packaging and publication. The student executed the recorded training experiments; Codex performed packaging checks. The submitter remains responsible for reviewing and understanding the work.

The baseline GPT, trainer, fixed evaluator, tokenizer, data and tests are reused from the DASE7506 starter. Dataset text is by Wikipedia contributors; WikiText-2 is attributed to Merity et al., *Pointer Sentinel Mixture Models* (2016), https://arxiv.org/abs/1609.07843. The starter identifies CC BY-SA 3.0 and GNU Free Documentation License for the data. Full notices and source revision are retained in the archive. No new license is asserted for classroom code.
