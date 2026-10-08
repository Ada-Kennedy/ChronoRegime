# ChronoRegime

**Is the Future Predictable? Modeling Future Predictability for Reliable Temporal Reasoning**

This repository contains the paper PDF and the accompanying dataset files provided for this release.

## Paper

[Read the paper](paper/ChronoRegime.pdf)

ChronoRegime studies whether historical temporal evidence justifies committing to a future factual answer. The paper introduces Confidence-Aware Temporal Reasoning (CTR), which estimates future predictability from temporal dynamics and regulates answer commitment accordingly.

## Repository contents

```text
paper/ChronoRegime.pdf
data/test.jsonl
data/increamental-cloze.jsonl
```

The PDF and dataset contents are preserved as supplied. The PDF has been renamed for a portable repository path; original dataset filenames are retained, including the spelling of `increamental-cloze.jsonl`.

## Dataset overview

Each non-empty line is a JSON object, encoded in UTF-8.

| File | Records | Values of the `split` field |
| --- | ---: | --- |
| `data/test.jsonl` | 337 | TEST: 280; DEV: 57 |
| `data/increamental-cloze.jsonl` | 32 | TRAIN: 4; TEST: 25; DEV: 3 |

Despite its filename, `test.jsonl` contains both TEST and DEV records. Use each record's `split` field when selecting a subset.

### Fields

| Field | Contents |
| --- | --- |
| `id` | Record identifier, stored as a string |
| `split` | Supplied split label: TRAIN, DEV, or TEST |
| `question` | Natural-language question |
| `cloze_question` | Cloze-form question, generally using `_X_` as a placeholder; absent in one incremental-file record |
| `effective_year_raw` | Original temporal specification |
| `effective_year_num` | Numeric temporal value as supplied |
| `next_review` | Review timing or change-point information as supplied |
| `false_premise` | Boolean false-premise label |
| `num_hops` | Reasoning-hop annotation; may be empty |
| `fact_type` | Temporal fact category |
| `source` | Source text or URL(s); may be empty |
| `answer_0`, `answer_1` | Supplied answer fields; may be empty |
| `before` | Additional prior-answer field, present in 17 incremental-file records |
| `next_answer` | Additional future-answer field in the incremental file; may contain `UNKNOWN` |

Annotations and answers are time-dependent and are preserved without updating them to current facts. Empty strings, missing keys, and the literal value `UNKNOWN` remain as provided.

## Load the data

Python standard library only:

```python
import json
from pathlib import Path

path = Path("data/test.jsonl")
with path.open(encoding="utf-8") as f:
    records = [json.loads(line) for line in f if line.strip()]

test_records = [row for row in records if row["split"] == "TEST"]
print(f"All records: {len(records)}; TEST records: {len(test_records)}")
```
## Citation

If you find this work useful, please cite our paper:

```bibtex
@inproceedings{huang2026futurepredictable,
  title     = {Is the Future Predictable? Modeling Future Predictability for Reliable Temporal Reasoning},
  author    = {Huang, Yongyi and Zhang, Huaping and Cui, Wenyao and Li, Qiuchi and Li, Lei and Zhang, Baohua},
  booktitle = {Proceedings of the 2026 Conference on Empirical Methods in Natural Language Processing},
  year      = {2026}
}
```

This citation is provisional. We will update it with the official proceedings metadata once available.

