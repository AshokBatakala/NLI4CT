# NLI4CT

The implementation of the system for SemEval-2023 Task 7: Natural Language Inference for Clinical Trials (NLI4CT).

**Safe Biomedical Natural Language Inference for Clinical Trials**
Batakala Ashok, Manish Nath, Shubham Gehlot
Indian Institute of Science, Bengaluru, India

## Abstract

Our study evaluates the performance of various LLMs on the NLI task on Clinical Trial data. We experimented with two prompting strategies: Chain-of-Thought (CoT) prompting, which encourages LLMs to generate step-by-step reasoning, and Zero-Shot prompting, which relies on the models' general language understanding capabilities without task-specific fine-tuning. We also experimented with different approaches for evidence retrieval.

## Dataset

The [NLI4CT dataset](https://sites.google.com/view/nli4ct/) is used. Each example consists of a Clinical Trial Report (CTR) — with sections such as Intervention, Eligibility (Inclusion/Exclusion Criteria), Results, and Adverse Events — paired with a hypothesis. The task is to infer whether the hypothesis is an `Entailment` or a `Contradiction` given the relevant evidence from the CTR.

## Approach

1. **Evidence Retrieval** — given a CTR section and a hypothesis, retrieve the sentences from that section relevant to the hypothesis.
2. **Inference** — prompt an LLM with the retrieved evidence and the hypothesis to predict `Entailment` or `Contradiction`.

Two prompting strategies were compared for inference:

- **Zero-shot prompt**: `Evidence: [Evidence] Statement: [Hypothesis] Question: Answer in one word, is the statement a contradiction or an entailment? Answer:`
- **Chain-of-Thought (CoT) prompt**: same as above, with `Let's think step by step.` appended to encourage step-by-step reasoning before the final answer.

## Experiments

- **Evidence retrieval models**: BERT, ClinicalBERT, BioBERT, and multi-qa-mpnet-base (Sentence-BERT with cosine similarity).
- **Inference LLMs**: ChatGPT 3.5, Gemini, and GPT-4-based Copilot, evaluated with both Zero-shot and CoT prompting, broken down by CTR section (overall, adverse events, eligibility, intervention, results).

### Evidence Retrieval Results

| Model | F1 score | Precision | Recall |
|---|---|---|---|
| BERT | 78.23 | 77.5 | 80.8 |
| ClinicalBERT | 81.1 | 81.0 | 81.2 |
| BioBERT | 80.4 | 78.0 | 81.9 |
| multi-qa-mpnet-base* | 52.9 | 53.2 | 52.6 |

\*Sentence-BERT, cosine similarity.

## Conclusion

- Among the various LLMs evaluated, the GPT-4-based Copilot consistently outperformed others, yielding the best results.
- On average, CoT performs better than Zero-shot, implying that the CoT prompting strategy promotes step-by-step reasoning in LLMs, helping them break the task into smaller, more manageable steps. This explicit reasoning likely enhances LLMs' understanding of Clinical Trial Reports, facilitating accurate inference of a hypothesis's alignment with the provided evidence.
- Performance varies across CTR sections; optimizing prompts specific to each section may give better results.

## Future Work

Optimize prompts specific to each CTR section to improve inference performance further.

## Note for Ashok:
server : `.182`
location : `/media/Ext_4T_SSD/ASHOK_NLP_DS207/NLI4CT_DS207`
conda env: `nlp_1`
