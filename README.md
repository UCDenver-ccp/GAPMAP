# GAPMAP — Mapping Scientific Knowledge Gaps in Biomedical Literature with LLMs

> Concise, clean README for the associated paper/repo. It keeps only the essentials: what the project is, how it works, what was evaluated, and the headline findings—using compact tables.

---

## TL;DR
GAPMAP shows that large language models (LLMs) can surface **explicit** (author‑signaled) and **implicit** (unstated, inferred) knowledge gaps in scientific articles. The work introduces **TABI**—an interpretable template *(Claim · Grounds → Warrant + confidence bucket)*—for implicit gaps. Larger models generally perform best; sentence‑aligned chunking of long text (~1K words) is safe and often helpful.

---

## What’s in this repository
- Baselines for **explicit** and **implicit** gap detection  
- **TABI** prompting template (*Claim*, *Grounds*, *Warrant*, *Bucket*)  
- Evaluation scripts: **ROUGE‑L F1** (explicit) and **entailment‑based accuracy** (implicit)  
- Small, reproducible result tables and comparisons

---

## Methods (short)
- **Explicit gaps:** detect uncertainty/negation cues in paragraphs/sections; score predictions against gold spans with ROUGE‑L F1 using one‑to‑one matching.  
- **Implicit gaps (TABI):** generate a **Claim**, cite supporting **Grounds**, add a **Warrant**, and assign a **confidence bucket**; judge correctness with bi‑directional entailment between predictions and gold premises/claims.  
- **Long context:** optional sentence‑aligned **~1K‑word chunking**; compare “no chunking” vs “chunked”.

---

## Datasets (2 explicit, 2 implicit)

| Task     | Dataset (unit)                                   | Domain & Scale (high level)                 |
|----------|---------------------------------------------------|---------------------------------------------|
| Explicit | IPBES (paragraphs)                               | Biodiversity; paragraph‑level gap spans     |
| Explicit | Scientific Challenges & Directions (sections)     | COVID‑19; sentences labeled within sections |
| Implicit | Manual implicit‑gap corpus (paragraphs)           | Biomedical; ~hundreds of paragraphs         |
| Implicit | Full‑text pilot (full papers + author survey)     | Mixed STEM; ~dozens of articles             |

---

## Evaluation

| Task/Setting                      | Metric                        | Notes                                                                 |
|----------------------------------|-------------------------------|-----------------------------------------------------------------------|
| Explicit (IPBES)                 | ROUGE‑L F1                    | Stemming + one‑to‑one matching with a similarity threshold            |
| Explicit (COVID‑19 sections)     | Accuracy                      | Validate predicted statements with an ignorance‑cue dictionary         |
| Implicit (paragraph level)       | Accuracy (entailment)         | Bi‑directional entailment between predicted claim/warrant and gold    |
| Long‑context robustness          | Comparison (no‑chunk vs chunk) | Sentence‑aligned ~1K‑word chunks; recall often improves                |

---

## Headline Results (compact)

**A) Explicit — IPBES (ROUGE‑L F1)**  
Large open‑weight and strong closed‑weight models are both competitive; best results come from the largest models. Chunking preserves performance.

**B) Explicit — COVID‑19 Sections (Accuracy)**  
Long sections are harder (single gold statement per section). The best closed‑weight large model leads, with chunking sometimes helping.

**C) Implicit — Paragraph Level (Accuracy)**  
Best performance from large closed‑weight models; large open‑weights are close behind. Smaller models struggle without few‑shot guidance.

**Key takeaways**
- **Scale helps** (bigger models win), but strong **open‑weight** models can be competitive.  
- **TABI** makes implicit gaps **interpretable** and easier to score.  
- **Chunking** is a reliable preprocessing step and often boosts recall.

---

## Quick start (repro outline)
1. **Prepare text** (paragraphs/sections/full text). Optionally chunk to **~1K words** on sentence boundaries.  
2. **Explicit task:** run model → extract candidate gap statements → score with **ROUGE‑L F1** (IPBES) or **accuracy** (COVID‑19).  
3. **Implicit task (TABI):** prompt using **Claim / Grounds / Warrant + Bucket** (few‑shot recommended) → score with **entailment‑based accuracy**.  
4. **Report:** aggregate P/R/F1 (explicit) and accuracy (implicit); compare no‑chunk vs chunked.

---

## Practical notes
- **Few‑shot** examples materially improve TABI outputs; zero‑shot tends to be vague.  
- COVID‑19 sections may contain **multiple gaps** though only one is labeled; numeric/contrastive cues matter, not just lexical hedges.  
- For deployment: keep a **human‑in‑the‑loop** and consider **domain adaptation**.

---

## Citation
**GAPMAP: Mapping Scientific Knowledge Gaps in Biomedical Literature Using Large Language Models.**  
(Add full bibliographic entry here.)

---

## License
Specify your license here (e.g., MIT).

## Contact
Maintainer name • email or GitHub handle.
