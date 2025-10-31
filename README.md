% README (LaTeX-friendly) — GAPMAP: Mapping Scientific Knowledge Gaps in Biomedical Literature Using LLMs

\section*{Project Title}
\textbf{GAPMAP: Mapping Scientific Knowledge Gaps in Biomedical Literature Using Large Language Models}. :contentReference[oaicite:0]{index=0}

\section*{One-paragraph Summary}
GAPMAP studies how large language models (LLMs) can automatically identify \emph{explicit} gaps (clearly stated unknowns) and \emph{implicit} gaps (unstated but inferable from context) in scientific text. It evaluates open- and closed-weight LLMs across paragraph- and document-level settings, and introduces \textbf{TABI} (Toulmin-Abductive Bucketed Inference) to structure reasoning for implicit gaps. Results show robust LLM capability for surfacing gaps, with larger models generally stronger. :contentReference[oaicite:1]{index=1}

\section*{Techniques}
\begin{itemize}
  \item \textbf{Explicit gap extraction}: detect lexical uncertainty/negation cues at sentence/paragraph scale; evaluate with ROUGE-L F1 one-to-one matching. :contentReference[oaicite:2]{index=2} :contentReference[oaicite:3]{index=3}
  \item \textbf{Implicit gap inference (TABI)}: cast as abductive NLI with a Toulmin-style template \emph{(Claim, Grounds $\rightarrow$ Warrant)} and a confidence \emph{Bucket} (more\_probable vs. least\_probable) for calibration and scoring. :contentReference[oaicite:4]{index=4} :contentReference[oaicite:5]{index=5}
  \item \textbf{Context handling}: evaluate with and without 1{,}000-word chunking to test long-context robustness. :contentReference[oaicite:6]{index=6}
\end{itemize}

\section*{Datasets}
Four public datasets spanning both gap types; nearly 1{,}500 documents, including a manually annotated biomedical corpus and a full-paper pilot. :contentReference[oaicite:7]{index=7}

\section*{Evaluation}
\begin{itemize}
  \item \textbf{Explicit (IPBES)}: ROUGE-L F1 with stemming; threshold 0.55; report P/R/F1. :contentReference[oaicite:8]{index=8}
  \item \textbf{Explicit (COVID-19)}: validate predicted statements with a domain ignorance-cues dictionary; report accuracy. :contentReference[oaicite:9]{index=9}
  \item \textbf{Implicit (paragraph-level)}: correctness if bi-directional entailment (RoBERTa-large) between predicted Claim/Warrant and gold premises/claims exceeds 0.4. :contentReference[oaicite:10]{index=10}
\end{itemize}

\section*{Headline Results (concise tables)}
\subsection*{Explicit Gaps — IPBES (ROUGE-L F1)}
\begin{tabular}{l c}
\hline
Model & F1 \\
\hline
Llama-3.3-70B & \textbf{0.8307} \\
GPT-5 & 0.7949 \\
GPT-4o Mini & 0.7907 \\
\hline
\end{tabular}
\quad
\begin{tabular}{l c}
\hline
Model (1K-word chunks) & F1 \\
\hline
GPT-4o Mini & \textbf{0.8143} \\
Llama-3.3-70B & 0.8138 \\
GPT-5 & 0.7947 \\
\hline
\end{tabular}

\noindent\emph{Takeaway:} open-weight models are competitive; chunking preserves or slightly boosts recall for some models. :contentReference[oaicite:11]{index=11}

\subsection*{Explicit Gaps — COVID-19 Sections (Accuracy)}
\begin{tabular}{l c}
\hline
Setting (Top Model) & Accuracy \\
\hline
1{,}000-word chunks (GPT-5) & \textbf{63.51\%} \\
No context limit (GPT-5) & \textbf{60.64\%} \\
\hline
\end{tabular}
\\
Style differences (single gold statement per section; numeric/contrastive cues) make this dataset harder than IPBES. :contentReference[oaicite:12]{index=12}

\subsection*{Implicit Gaps — Paragraph Level (Accuracy)}
\begin{tabular}{l c}
\hline
Model & Acc. \\
\hline
GPT-5 & \textbf{84.43\%} \\
GPT-4o & 80.66\% \\
GPT-4o Mini & 80.66\% \\
Llama-3.3-70B & 77.89\% \\
\hline
\end{tabular}
\\
Bucketed confidence supports calibration/analysis of correct matches. :contentReference[oaicite:13]{index=13}

\section*{Conclusion}
LLMs can systematically surface both explicit and implicit knowledge gaps in biomedical literature. TABI provides structured, inspectable reasoning for implicit gaps, and chunking is a practical preprocessing strategy. Larger models perform best overall; human-in-the-loop verification and expanded benchmarks are recommended for deployment. :contentReference[oaicite:14]{index=14} :contentReference[oaicite:15]{index=15}
