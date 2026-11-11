CLASSICAL REASONING ASSIGNMENT

Submission contents
- reasoning_agent.ipynb: complete implementation, dataset downloaders, evaluation, and submission.csv generation.
- report.pdf: system design, algorithms, data sources, evaluation protocol, and limitations.
- submission.csv: header template; the notebook fills it with id,label predictions when run.
- README.txt: these instructions.

Run
1. Open reasoning_agent.ipynb in Jupyter or Google Colab.
2. Run all cells from top to bottom. Internet access is required to download the public data.
3. The notebook installs datasets and huggingface_hub in its first setup cell.
4. It downloads RuleTaker from jise/ruletaker (train and test), FOLIO validation, and the two CounterBench JSON files from CounterBench/CounterBench.
5. It prints accuracy, coverage, unsupported records, and total/average inference time, then writes evaluation_results.json and submission.csv.

FOLIO access
The Hugging Face yale-nlp/FOLIO repository requires accepting its access conditions. Set HF_TOKEN after access is granted. If Hugging Face access is unavailable, the notebook downloads the matching folio-v0.0 validation JSONL from the original Yale-LILY FOLIO repository. It does not substitute a different dataset.

Private data
For private labelled evaluation, place a JSONL/JSON file at private_dev.jsonl. For private predictions, place an unlabelled JSONL/JSON file at private_test.jsonl. The notebook automatically uses these files when present. Otherwise it evaluates the public development sources and creates a demonstration submission.csv from the public RuleTaker test split.

Generic structured record schema
Each record contains id, facts, rules, and query. Add label only for labelled development data. Each fact is an atom represented as a list; each rule is [body_atoms, head_atom]; variables start with ?. Alternatively, provide source-native records for RuleTaker (context/statement), FOLIO (premises-FOL/conclusion-FOL), or CounterBench (given_info/question); the notebook detects these formats automatically.

Interpretation
Accuracy is calculated only on records the reasoner successfully handles. Coverage and unsupported counts are reported separately. Do not report scored-record accuracy as full-dataset accuracy if coverage is below 100%. Unsupported examples are not assigned an invented False label. The notebook contains no hard-coded benchmark examples or synthetic fallback dataset.
