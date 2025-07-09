# Master-Thesis-Shouvik

This repository supports my Master's thesis:  
# "Evaluating the Effectiveness of Large Language Models in Named Entity Extraction."

The study explores how LLMs and transformer-based models perform on NER tasks across different domains: **noisy social media** vs **formal newswire**. To this end, two standard benchmarks are used:

1. [WNUT 2017 (tner/wnut2017)](https://huggingface.co/datasets/tner/wnut2017) — User-generated, informal text  
2. [CoNLL 2003 (tner/conll2003)](https://huggingface.co/datasets/tner/conll2003) — Formal, well-edited newswire articles

---

## 📊 Dataset Overview

### 1. WNUT 2017

- **Source:** [tner/wnut2017](https://huggingface.co/datasets/tner/wnut2017)
- **Domain:** Noisy, social media (e.g., Twitter)
- **Entity Types:** `person`, `location`, `corporation`, `product`, `creative-work`, `group`
- **Challenges:** Misspellings, slang, hashtags, irregular grammar

### 2. CoNLL 2003

- **Source:** [tner/conll2003](https://huggingface.co/datasets/tner/conll2003)
- **Domain:** Newswire articles (Reuters)
- **Entity Types:** `PER`, `LOC`, `ORG`, `MISC`
- **Strengths:** Clean, grammatically consistent language

---

## 📅 Project Plan & Experiment Overview

The following table outlines all major model configurations and experimental settings used in the thesis:

| Model Type         | Model Name(s)                           | Size     | Task Type              | Training Set | Evaluation Set | Experiment Setting     | Purpose                                             |
|--------------------|------------------------------------------|----------|-------------------------|--------------|----------------|------------------------|-----------------------------------------------------|
| Baseline           | BERT-base-cased                          | Small    | Token classification    | CoNLL-2003   | CoNLL-2003     | In-domain Supervised   | Traditional benchmark on clean, formal text         |
| Baseline           | BERT-base-cased                          | Small    | Token classification    | WNUT-17      | WNUT-17        | Noisy-domain Supervised| Baseline on informal, noisy social media text       |
| Baseline           | RoBERTa-base                             | Medium   | Token classification    | CoNLL-2003   | CoNLL-2003     | In-domain Supervised   | Compare with BERT baseline                         |
| Baseline           | RoBERTa-base                             | Medium   | Token classification    | WNUT-17      | WNUT-17        | Noisy-domain Supervised| Check robustness on noisy text                     |
| LLM Prompt-based   | T5-small                                 | Small    | Prompt → Entities       | None         | CoNLL/WNUT     | Zero-shot              | See how a tiny model handles entity extraction      |
| LLM Prompt-based   | FLAN-T5-base                             | Medium   | Prompt → Entities       | None         | CoNLL/WNUT     | Zero-shot              | Text-to-text few-shot/zero-shot comparison         |
| LLM Prompt-based   | Mistral-7B-Instruct                      | Medium   | Instruction generation  | None         | CoNLL/WNUT     | Zero-shot              | Instruction-following LLM in zero-shot setting     |
| LLM Prompt-based   | Mixtral-8x7B (MoE) / LLaMA-2-13B         | Large    | Instruction generation  | None         | CoNLL/WNUT     | Zero-shot              | Effect of scale in zero-shot setting               |
| LLM Fine-tuned     | T5-small                                 | Small    | Prompt → Entities       | CoNLL-2003   | CoNLL/WNUT     | LoRA Fine-tuned        | Light-weight fine-tuning analysis                  |
| LLM Fine-tuned     | FLAN-T5-base                             | Medium   | Prompt → Entities       | CoNLL-2003   | CoNLL/WNUT     | LoRA Fine-tuned        | Fine-tuned performance vs prompting                |
| LLM Fine-tuned     | Mistral-7B-LoRA                          | Medium   | Instruction generation  | CoNLL-2003   | CoNLL/WNUT     | LoRA Fine-tuned        | Domain shift generalization                        |
| LLM Fine-tuned     | Mixtral-LoRA / LLaMA-2-13B-LoRA          | Large    | Instruction generation  | CoNLL-2003   | CoNLL/WNUT     | LoRA Fine-tuned        | Large-scale generalization to noisy domain         |
| LLM Few-shot       | T5, Mistral, Mixtral (varied sizes)      | S/M/L    | Prompt → Entities       | None         | WNUT-17        | Few-shot prompting     | In-context learning across model sizes             |
| Cross-domain       | BERT / LLMs (all sizes)                  | CoNLL-2003| WNUT-17        | Domain Shift            | Evaluate generalization from clean → noisy domain  |

---

## 🧪 Experimental Objectives

These experiments aim to answer the following key questions:

- Can zero-shot prompting with large LLMs match traditional supervised fine-tuning?
- How well do LLMs handle domain shifts (e.g., from clean to noisy)?
- What’s the trade-off between model size, data needs, and performance?
- Are instruction-based models more adaptable than token classifiers?

---

## 📎 Useful Links

- 📘 WNUT 2017 Dataset: [https://huggingface.co/datasets/tner/wnut2017](https://huggingface.co/datasets/tner/wnut2017)  
- 📙 CoNLL 2003 Dataset: [https://huggingface.co/datasets/tner/conll2003](https://huggingface.co/datasets/tner/conll2003)  
- 🏁 WNUT 2017 Shared Task: [https://noisy-text.github.io/2017/emerging-rare-entities.html](https://noisy-text.github.io/2017/emerging-rare-entities.html)  
- 🧪 T-NER GitHub Repo: [https://github.com/asahi417/tner](https://github.com/asahi417/tner)

---

> 📌 _This repository provides all training scripts, fine-tuning configurations, prompts, evaluation metrics, and visualizations used in the thesis._
