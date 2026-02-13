# Feb 12 DOB NOW Experiment (Baseline vs Multi-Agent Review Board)

Task:
Given DOB NOW permit Job Description text, predict whether the job involves electrification / decarbonization assets.

Input:
- Column: input (DOB NOW job description text)

Outputs:
We compare two systems:
1) Baseline single-model: R1_meta-llama/Llama-3.2-3B-Instruct
2) Multi-agent review board (2 rounds): R2_* outputs from Llama + Qwen + Gemma, aggregated by majority vote.

Ground Truth:
- Column: ground_truth (YES/NO label)

Hallucination Definition (automatic checks):
Flag hallucination if the model output claims equipment terms (heat pump, EV charger, solar, VRF, etc.)
that do not appear in the input text. Also flag if an Evidence_Quote is provided that is not a substring
of the input (when present).

Metrics:
- Accuracy, Precision, Recall, F1 (positive class = YES)
- Hallucination rate (baseline vs board)
- n_eval (rows where gt and prediction exist)

Artifacts:
- dob_review_board_results.csv (per-row outputs + hallucination flags)
- dob_tiny_results_table.csv (summary metrics table)
- dob_review_board_analysis.ipynb (analysis notebook)

