# GAPMAP â€” Mapping Scientific Knowledge Gaps in Biomedical Literature with LLMs

> Concise, clean README for the associated paper/repo. It keeps only the essentials: what the project is, how it works, what was evaluated, and the headline findingsâ€”using compact tables.

---

## TL;DR
GAPMAP shows that large language models (LLMs) can surface **explicit** (authorâ€‘signaled) and **implicit** (unstated, inferred) knowledge gaps in scientific articles. The work introduces **TABI**â€”an interpretable template *(Claim Â· Grounds â†’ Warrant + confidence bucket)*â€”for implicit gaps. Larger models generally perform best; sentenceâ€‘aligned chunking of long text (~1K words) is safe and often helpful.

---

## Whatâ€™s in this repository
- Baselines for **explicit** and **implicit** gap detection  
- **TABI** prompting template (*Claim*, *Grounds*, *Warrant*, *Bucket*)  
- Evaluation scripts: **ROUGEâ€‘L F1** (explicit) and **entailmentâ€‘based accuracy** (implicit)  
- Small, reproducible result tables and comparisons

---

## Methods (short)
- **Explicit gaps:** detect uncertainty/negation cues in paragraphs/sections; score predictions against gold spans with ROUGEâ€‘L F1 using oneâ€‘toâ€‘one matching.  
- **Implicit gaps (TABI):** generate a **Claim**, cite supporting **Grounds**, add a **Warrant**, and assign a **confidence bucket**; judge correctness with biâ€‘directional entailment between predictions and gold premises/claims.  
- **Long context:** optional sentenceâ€‘aligned **~1Kâ€‘word chunking**; compare â€œno chunkingâ€ vs â€œchunkedâ€.

---

## Datasets (2 explicit, 2 implicit)

| Task     | Dataset (unit)                                   | Domain & Scale (high level)                 |
|----------|---------------------------------------------------|---------------------------------------------|
| Explicit | IPBES (paragraphs)                               | Biodiversity; paragraphâ€‘level gap spans     |
| Explicit | Scientific Challenges & Directions (sections)     | COVIDâ€‘19; sentences labeled within sections |
| Implicit | Manual implicitâ€‘gap corpus (paragraphs)           | Biomedical; ~hundreds of paragraphs         |
| Implicit | Fullâ€‘text pilot (full papers + author survey)     | Mixed STEM; ~dozens of articles             |

---

## Evaluation

| Task/Setting                      | Metric                        | Notes                                                                 |
|----------------------------------|-------------------------------|-----------------------------------------------------------------------|
| Explicit (IPBES)                 | ROUGEâ€‘L F1                    | Stemming + oneâ€‘toâ€‘one matching with a similarity threshold            |
| Explicit (COVIDâ€‘19 sections)     | Accuracy                      | Validate predicted statements with an ignoranceâ€‘cue dictionary         |
| Implicit (paragraph level)       | Accuracy (entailment)         | Biâ€‘directional entailment between predicted claim/warrant and gold    |
| Longâ€‘context robustness          | Comparison (noâ€‘chunk vs chunk) | Sentenceâ€‘aligned ~1Kâ€‘word chunks; recall often improves                |

---

## Headline Results (compact)

**A) Explicit â€” IPBES (ROUGEâ€‘L F1)**  
Large openâ€‘weight and strong closedâ€‘weight models are both competitive; best results come from the largest models. Chunking preserves performance.

**B) Explicit â€” COVIDâ€‘19 Sections (Accuracy)**  
Long sections are harder (single gold statement per section). The best closedâ€‘weight large model leads, with chunking sometimes helping.

**C) Implicit â€” Paragraph Level (Accuracy)**  
Best performance from large closedâ€‘weight models; large openâ€‘weights are close behind. Smaller models struggle without fewâ€‘shot guidance.

**Key takeaways**
- **Scale helps** (bigger models win), but strong **openâ€‘weight** models can be competitive.  
- **TABI** makes implicit gaps **interpretable** and easier to score.  
- **Chunking** is a reliable preprocessing step and often boosts recall.

---

## Quick start (repro outline)
1. **Prepare text** (paragraphs/sections/full text). Optionally chunk to **~1K words** on sentence boundaries.  
2. **Explicit task:** run model â†’ extract candidate gap statements â†’ score with **ROUGEâ€‘L F1** (IPBES) or **accuracy** (COVIDâ€‘19).  
3. **Implicit task (TABI):** prompt using **Claim / Grounds / Warrant + Bucket** (fewâ€‘shot recommended) â†’ score with **entailmentâ€‘based accuracy**.  
4. **Report:** aggregate P/R/F1 (explicit) and accuracy (implicit); compare noâ€‘chunk vs chunked.

---

## Practical notes
- **Fewâ€‘shot** examples materially improve TABI outputs; zeroâ€‘shot tends to be vague.  
- COVIDâ€‘19 sections may contain **multiple gaps** though only one is labeled; numeric/contrastive cues matter, not just lexical hedges.  
- For deployment: keep a **humanâ€‘inâ€‘theâ€‘loop** and consider **domain adaptation**.

---

## Citation
**GAPMAP: Mapping Scientific Knowledge Gaps in Biomedical Literature Using Large Language Models.**  
(Add full bibliographic entry here.)

---

## License
Specify your license here (e.g., MIT).

## Contact
Maintainer name â€¢ email or GitHub handle.
