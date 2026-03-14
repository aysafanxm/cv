# Detailed Project Tasks Reference — Aysa X. Fan

A comprehensive list of tasks performed across PhD research projects, organized by project. Use this as a reference when tailoring your CV, cover letters, or research statements.

---

## 1. Dissertation: Comparative Study of Code-Tracing Learning Approaches (in progress)

### Study Design & IRB
- Designed a three-condition mixed-methods randomized experiment comparing instructional approaches for teaching code tracing to introductory CS students (CS 105 at UIUC)
- Prepared and submitted IRB application (IRB25-1481); obtained approval for ~30-100 participants (still on-going)
- Designed consent forms and recruitment materials

### Curriculum Development
- Developed a three-stage progressive curriculum ("How to Trace," "Why to Trace," "What to Trace") with 10+ scaffolded learning activities
- **Stage 1 (How to Trace):** Created questions on building tracing tables for variables, loops, conditionals, and functions
- **Stage 2 (Why to Trace):** Designed debugging scenarios where students trace buggy code (e.g., sum positives, max finding, list reverse) to find discrepancies between expected and actual behavior
- **Stage 3 (What to Trace):** Developed activities requiring students to strategically select which variables to track and build trace tables for analysis
- Authored all question content, scoring rubrics, and point allocations (80-point activity)
- Designed a separate control group activity (10 "How to Trace" level questions with correctness-only feedback)

### LLM Feedback System
- Built and self-hosted an LLM-powered feedback website that provides automated, context-aware tutoring responses to students during learning activities (Treatment Group B)
- Designed prompts for the LLM feedback system to provide pedagogically appropriate hints without giving away answers
- Integrated LLM feedback with the learning activity so students can interact with the tutor at each stage

### Platform & Integration
- Implemented the end-to-end learning activity on PrairieLearn, including all question types (tracing tables, fill-in-the-blank, multiple choice, free response)
- Built the integration between PrairieLearn and the self-hosted LLM feedback website
- Set up data collection pipelines to capture student responses, interaction logs, and LLM conversation histories

### Assessment & Data Collection
- Designed pre-test and post-test instruments to measure code tracing skill improvement
- Designed post-activity survey to capture student experience and perceptions
- Managing participant recruitment, consent, scheduling, and data collection within a single-semester timeline
- Planned both quantitative (pre/post comparison) and qualitative (student-LLM interaction analysis) analyses

---

## 2. LLM-Based Classification of Debugging Strategies

**Publications:** ICQE 2024 (Best Student Paper Nominee); JEDM (under review, 2025)

### Codebook Development
- Conducted a literature review identifying 22 candidate debugging strategies from prior research
- Refined candidate strategies through expert discussion sessions to consolidate similar strategies and remove those not observable in submission data
- Narrowed to 10 candidate strategies for annotation; further refined to 4 retained strategies (Focusing on Problem, Iterative Changes, Tracing, Starting Over) plus "No Strategy"
- Developed full operational definitions with annotation criteria for each strategy
- Established aggregation rules (e.g., strategy must appear at least twice between submission pairs to be labeled as present for the episode)

### Data Annotation (4 Phases, 2,350 Episodes)
- **Phase 1 — Initial Annotation:** Collaboratively coded 220 episodes in batches of 20, comparing annotations and refining strategy definitions after each batch; achieved IRR (κ > 0.75) for common strategies (Focusing on Problem, Iterative Changes)
- **Phase 2 — IRR Establishment:** Independently coded an additional 220 episodes; confirmed satisfactory IRR for common strategies; reconciled disagreements to produce 453 total episodes with agreed-upon labels
- **Phase 3 — Common Strategy Annotation:** Independently coded 732 additional episodes for common strategies (single-annotator after IRR established)
- **Phase 4 — Rare Strategy Annotation:** Used LLM-based filtering to surface rare strategy candidates; annotated 274 LLM-filtered episodes across three rounds (78 for both rare strategies, then 114 and 82 focusing on starting over and tracing respectively); achieved IRR: tracing κ = 0.88, starting over κ = 0.82; then independently coded 891 additional episodes
- Participated in all inter-rater reliability discussions and calibration sessions throughout

### LLM-Based Filtering Pipeline (ICQE 2024)
- Designed an LLM-based filtering approach using GPT-4o to pre-screen episodes for rare debugging strategies (tracing and starting over)
- Developed filtering prompts by eliciting the hierarchical decision-making processes of expert annotators (decision map / flowchart)
- Achieved 84% recall for tracing and 95% recall for starting over in filtering
- Inflated rare strategy occurrence from ~4% to 27–40% in annotation samples, reducing manual annotation effort by ~75%
- This approach enabled annotators to achieve acceptable IRR for rare strategies that were previously too infrequent to calibrate on

### Annotation Tool Development
- Built a custom browser-based annotation tool for expert labeling
- Tool displays the programming problem, two consecutive submissions side-by-side with visual diff highlighting (red: removed code, green: added code), error feedback for each submission, and strategy checkboxes
- Tool supports sequential navigation through episodes and submission pairs

### LLM Benchmarking (JEDM under review)
- Benchmarked seven LLMs on multi-label debugging strategy classification:
  - Six open-source models: GLM-4-32B, Qwen3-30B, Mistral-Small-3.1-24B, Qwen3-14B, Llama-3.1-8B, Phi-4-mini
  - One commercial model: Claude Sonnet 4.5 (via Anthropic API)
- All open-source models run locally on NVIDIA A100 (80GB) GPUs with guided decoding for structured JSON output
- Used deterministic inference (temperature=0) across all models for reproducibility

### Prompt Engineering (4 Iterative Prompts)
- Developed four structurally distinct prompt strategies through iterative error analysis on 1,255 development episodes (non-overlapping batches of ~300 per round):
  - **Prompt 1 — Direct Definition Mapping:** Presented each strategy definition independently
  - **Prompt 2 — Hierarchical Expert Flow:** Implemented the expert's cognitive workflow as a sequential filtering decision tree with implicit chain-of-thought reasoning
  - **Prompt 3 — Contrastive Definitions:** Stated what constitutes and what does *not* qualify for each strategy to clarify boundary conditions
  - **Prompt 4 — Balanced Hierarchical-Contrastive:** Combined hierarchical flow with selective contrastive elements
- Used GPT-4o (not the evaluated models) for prompt optimization to prevent evaluation bias
- Designed structured function-call style output format for consistent parsing across models

### Fine-Tuning
- Fine-tuned Qwen3 models (0.6B, 8B, 14B parameters) using Self-Taught Reasoner (STaR) method with iterative self-improvement over 10 iterations
- STaR process: initial reasoning generation → strategy aggregation → feedback loop (correct/incorrect without revealing ground truth) → iterative refinement → data augmentation → model fine-tuning
- Fine-tuned three encoder baselines: BERT-base (110M), RoBERTa-base (125M), ModernBERT-base (149M) on the 1,355-episode development set

### Evaluation & Statistical Analysis
- Evaluated all models on a held-out 995-episode evaluation set
- Computed macro-averaged precision, recall, F1, and Cohen's κ (per-strategy and aggregated) using scikit-learn
- Implemented label-space filtering to handle partial annotations across different strategy subsets
- Computed 95% bootstrap confidence intervals via non-parametric resampling (1,000 iterations)
- Performed McNemar's tests for pairwise model comparison on per-strategy binary classification
- Used Wilcoxon signed-rank tests to compare models across four prompting strategies
- Stratified train/test split using scikit-learn's StratifiedGroupKFold to preserve class proportions

---

## 3. LLM-Generated Code-Tracing Questions

**Publications:** EMNLP 2023 (Findings); SIGCSE 2024 (Poster)

### Dataset Curation (EMNLP 2023)
- Sourced 158 unique code-tracing questions from CSAwesome (AP Computer Science A curriculum)
- Added 18 questions extracted from relevant YouTube videos to enhance diversity
- Examined other platforms (various sources) but excluded them due to lack of explicit tracing questions
- Final dataset: 176 unique code snippets paired with human-authored tracing questions
- Published the dataset and code on GitHub for community use

### Prompt Engineering & Model Selection (EMNLP 2023)
- Iteratively refined prompts for GPT-3.5-turbo and GPT-4, adopting an expert instructor's perspective to encourage deep understanding via code-tracing questions
- Compared zero-shot and few-shot generation approaches
- Used BERTScore to assess question diversity and similarity between LLM-generated and human-authored questions
- Found that few-shot generation introduced significant bias toward example questions, narrowing diversity; selected zero-shot generation for broader question variety
- Used regular expressions in post-processing to segment generated content and isolate individual tracing questions
- Selected GPT-4 based on more balanced BERTScore performance (Precision ~0.6, Recall ~0.55, F1 ~0.5)

### Human Evaluation Design (EMNLP 2023)
- Designed a human evaluation framework with five criteria: relevance to learning objectives (1–5), tracing or not (yes/no), clarity (1–5), difficulty level (1–5), relevance to code snippet (1–5), authorship discernibility (human/AI), preference
- Recruited and coordinated four expert evaluators (CS graduate students with 1+ year teaching/tutoring experience)
- Each evaluator rated 44 randomly selected code snippets (from pool of 176) with paired questions (one human, one GPT-4) in randomized, blind order
- Designed and distributed evaluation questionnaires

### Statistical Analysis (EMNLP 2023)
- Applied Mann-Whitney U tests to compare median ratings across four evaluation criteria
- Found significant differences in relevance to learning objectives (p=0.047), clarity (p=0.011), and difficulty appropriateness (p=0.015), but no difference in relevance to code snippet (p=0.595)
- Despite statistical differences, practical quality differences were minimal (median ratings nearly identical)
- Built confusion matrices for authorship attribution: 56% of GPT-4 questions were mistakenly identified as human-created; 20% of human questions were misattributed to GPT-4
- Computed BLEU, ROUGE-1/2/L, and BERTScore to compare textual similarity between randomly selected GPT-4 and corresponding human questions (low BLEU=0.02, moderate BERTScore F1=0.303, confirming GPT-4 generates distinct, non-verbatim questions)

### Refined Prompt Design (SIGCSE 2024)
- Identified quality features of code tracing questions from literature: complexity, guessability, appropriate difficulty, reverse tracing, clarity, code relevance, edge cases, multiple answers
- Categorized features into "Utilized" (directly embedded in prompts) and "Observed" (expected to emerge naturally from code context)
- Designed expert-guided prompts incorporating these features, asking the LLM to justify each question's motivation
- Added chain-of-thought self-selection: LLM drafts explanations for each question, then selects the best ones based on "good question features"
- Coordinated expert evaluation (CS educator with 5+ years' experience) comparing new questions against previously preferred ones using expanded criteria (complexity, reverse-tracing inclusion, concept keywords, difficulty, edge cases, guessability, preference)
- Results: improved complexity (3.5 vs. 2.5), increased reverse-tracing coverage (83% vs. 0%), more concept keyword mentions (33% vs. 17%); marginally higher expert preference for new questions (42% vs. 33%)

---

## 4. LLM-Generated Code Comments for Novice Programmers

**Publication:** LLM4Ed Workshop at AIED 2024

### Dataset & Prompting
- Selected the LeetCode Java Solution dataset (30 "easy" level problems) aligned with introductory CS education
- Designed prompts for three LLMs (GPT-4, GPT-3.5-Turbo, Llama2) to generate instructional code comments
- Prompts structured to request: code chunking by functionality, high-level overview (rationale, complexity, approach), detailed step-by-step comments, and additional appropriate annotations
- Used expert-written inline documentation from LeetCode solutions as the human baseline

### Codebook Development & Expert Evaluation
- **Phase 1:** Developed a comprehensive codebook with eight Likert-scale criteria derived from literature: explains concepts used, identifies beginner mistakes, provides detail, clarifies code behavior, breaks down tasks, avoids jargon, explains before code, simple vocabulary
- Coordinated four experts (3+ years' programming and CS education experience) for blind evaluation
- **Phase 2:** Refined evaluation with binary criteria (high-level overview, logic before details, discuss complexity, connect concepts to context, warn potential mistakes, explain concept choice, provide inline comments, consistent style, explain code implementation, separate code chunks, simple language) plus a qualitative "friendly tutor" measure
- Introduced paired and global Likert ratings for objectivity

### Statistical Analysis
- Performed Kruskal-Wallis H tests across all four sources (GPT-4, GPT-3.5, Llama2, human expert) on eight first-round criteria
- Conducted pairwise Kruskal-Wallis comparisons for all model pairs across all criteria
- Performed chi-square analyses on binary criteria: found GPT-4 significantly outperformed Llama2 in discussing complexity (χ²=11.40, p=0.001) and connecting concepts to context (χ²=6.42, p=0.011)
- Found no significant differences between GPT-4 and human experts on any criterion
- Conducted Mann-Whitney U tests on "friendly tutor" ratings: GPT-4 outperformed GPT-3.5 (U=300.5, p=0.0017) and Llama2 (U=322.5, p=0.0003)

---

## 5. Lab Research on Novice Programming Behaviors (Contributing Author)

### Contributions across multiple lab publications (2021–2023)
- Contributed to feature design and interpretation for studies analyzing longitudinal programming log data from CS 125 at UIUC (745 students, 69 Java homework problems)
- Participated in research on debugging behavior dimensions, learner persistence, and performance modeling
- Contributed to data processing and analysis for studies using latent profile analysis, problem similarity/order-based weighting, and programming trace analysis

**Related publications (contributing author):**
- Zhang et al., 2023 — Problem similarity/order-based weighting for learner performance (JEDM)
- Zhang et al., 2023 — Latent profile analysis and programming traces for debugging (Education and Information Technologies)
- Zhang et al., 2023 — Dimensions of novices' code-writing skill (Computer Applications in Engineering Education)
- Pinto et al., 2023 — Programming experience and debugging behaviors (ICQE, Best Student Paper Nominee)
- Pinto et al., 2021 — Student persistence in introductory CS (CSEDM Workshop)

---

## Summary of Key Skills Demonstrated Across Projects

| Skill Area | Projects |
|---|---|
| Prompt engineering | All LLM projects (dissertation, JEDM, EMNLP, SIGCSE, AIED) |
| Data annotation & codebook development | JEDM, EMNLP, AIED |
| Inter-rater reliability calibration | JEDM (4 phases), EMNLP |
| LLM benchmarking & evaluation | JEDM (7 models), AIED (3 models + human) |
| Fine-tuning (STaR, encoder models) | JEDM |
| Statistical analysis | All projects (Mann-Whitney U, Kruskal-Wallis, chi-square, McNemar, bootstrap CI, Cohen's κ) |
| Tool/platform development | Dissertation (PrairieLearn + LLM website), JEDM (annotation tool) |
| Experimental design & IRB | Dissertation |
| Dataset curation & release | EMNLP (176 question pairs, GitHub) |
| Mixed-methods research | Dissertation, JEDM |
