Here are the things I'm uncertain about or couldn't fully determine from the papers. Grouped by project:

**Dissertation:**
1. What tech stack did you use for the self-hosted LLM feedback website? (e.g., Flask/Django, which LLM backend, how it's hosted -- local server, cloud, etc.)
2. How did you implement the PrairieLearn integration? Did you write custom PrairieLearn elements/questions, or use existing question types?
3. Are there any data processing or analysis pipelines you've already built for this study (e.g., log parsing, response scoring)?

**Debugging Classification (ICQE/JEDM):**
4. The browser-based annotation tool -- what did you build it with? (Python/Flask? JavaScript/React? Something else?)
5. For the LLM benchmarking, did you write the full inference pipeline yourself (e.g., setting up vLLM/SGLang on the A100, writing the batch inference scripts, parsing outputs)?
6. For the STaR fine-tuning, did you implement the full training loop yourself? What tools did you use (Unsloth, HuggingFace transformers, etc.)?

**Code Tracing Questions (EMNLP/SIGCSE):**
7. Did you write the code for the BERTScore evaluation pipeline and the post-processing (regex extraction of questions)?
8. Did you design and distribute the evaluation questionnaires yourself (e.g., Google Forms, Qualtrics)?

**Code Comments (AIED):**
9. How much of this project did you lead vs. collaborate on? Did you write the analysis scripts (chi-square, Kruskal-Wallis, Mann-Whitney U)?
10. Did you run the Llama2 inference locally, or use an API?

**General:**
11. Is there anything else you built or did across these projects that I haven't captured -- e.g., data cleaning pipelines, visualization tools, any teaching/mentoring of junior annotators?