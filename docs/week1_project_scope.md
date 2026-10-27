Here are all 10 items for SafePaper. Placeholders are marked with [ ].

## 1. Project Name and Domain
**SafePaper: a Research Paper Assistant with Prompt-Injection Screening**
**Domain:** Education and research support (literature review), with an AI security focus.

## 2. Problem Statement
Students doing literature reviews must read many long, dense papers just to find one method, dataset or result, and the answer to a single question is often spread across several papers. An AI assistant can answer these questions in plain English, which keyword search cannot do because it can only find pages, not combine answers. However, an assistant that reads outside documents can be manipulated by instructions hidden inside them (indirect prompt injection). SafePaper answers questions from a small set of papers with sources, and screens each retrieved passage before the AI uses it.

## 3. Evidence of the Problem
- NIST's 2025 report on adversarial machine learning (AI 100-2e2025) classifies prompt injection, both direct and indirect, as an attack on generative AI systems.
- Greshake et al. (2023) showed that attackers can plant instructions in content an AI application retrieves, and the application may follow them.
- The OWASP Top 10 for LLM Applications lists prompt injection among the main risks of building LLM apps.
- Debenedetti et al. (2024), AgentDojo, provides a benchmark for measuring how often agents are hijacked by injected instructions in the data they read.

## 4. Initial Related Work
| Study / solution | What it does | Limitation |
|---|---|---|
| Manual reading + PDF keyword search | Reliable and fully controlled by the reader | Slow, and cannot combine answers across papers |
| Basic RAG assistants (retrieve chunks, then answer) | Answers are grounded in documents | Usually trust all retrieved text, so planted instructions pass through |
| Llama Guard (Inan et al., 2023) | Classifies the safety of LLM inputs and outputs | Built for content moderation, not specifically for instructions hidden in retrieved documents |
| Spotlighting (Hines et al., 2024) | Marks untrusted text so the model treats it as data | Depends on the model following the markings, and is not a separate check |
| AgentDojo (Debenedetti et al., 2024) | Benchmark for attacks and defences on tool-using agents | Evaluates agents, but is not a ready-made assistant for students |

## 5. Engineering Gap / Limitation
Basic document Q&A systems pass retrieved text straight to the model, so one planted instruction can change the assistant's behaviour. Existing defences are often built for other settings (content moderation, tool-using agents) and are rarely tested on a small, local, student-scale assistant. This project adds a lightweight screening step and measures what it gains and what it costs: security (attacks blocked), answer quality (accuracy), false blocks, and speed.

## 6. Project Objectives
- **O1:** Design a document-grounded Q&A assistant over 3 open-access papers.
- **O2:** Develop it with retrieval and a rule-based safety checker, with an optional small local validator model.
- **O3:** Evaluate answer accuracy, share of planted attacks blocked, false blocks on normal text, and response time with and without the checker.

## 7. Target Users
Undergraduate and postgraduate students doing literature reviews on LLM agent security. The secondary users are their supervisors, who may want to check the sources behind an answer.

## 8. Data Sources
1. Greshake et al. (2023), *Not what you've signed up for: Compromising Real-World LLM-Integrated Applications with Indirect Prompt Injection*: https://arxiv.org/abs/2302.12173
2. Debenedetti et al. (2024), *AgentDojo: A Dynamic Environment to Evaluate Prompt Injection Attacks and Defenses for LLM Agents*: https://arxiv.org/abs/2406.13352
3. Vassilev et al. (2025), *Adversarial Machine Learning: A Taxonomy and Terminology of Attacks and Mitigations*, NIST AI 100-2e2025: https://csrc.nist.gov/pubs/ai/100/2/e2025/final

Optional background reference: OWASP Top 10 for LLM Applications, https://genai.owasp.org/llm-top-10/

Paper 3 is long, so you could limit it to the generative AI sections. I checked the NIST link and its details. Please open the arXiv links yourself before submitting, since I haven't verified them.

## 9. Comparison with EduAdvisor
**Similar**
- Both are document-grounded Q&A assistants built on public documents.
- Both are information-only, have a clear user group, and can be evaluated objectively.
- Both use retrieval plus guardrails.

**Different**
- **Documents:** EduAdvisor uses university PDFs (catalogue, handbook, graduation rules). SafePaper uses 3 open-access research papers.
- **Users:** EduAdvisor serves students planning courses. SafePaper serves students doing literature reviews.
- **Guardrails:** EduAdvisor's are generic. SafePaper has a specific checker for hidden instructions, tested with planted synthetic attacks.
- **Evaluation:** EduAdvisor measures answer quality, groundedness, latency and safety. SafePaper adds attack blocking rate and false blocks as measurable security results.

## 10. Responsible AI Risks
1. **Wrong or made-up answers (hallucination):** the assistant may state something the papers don't say, which could mislead a literature review. *Mitigation:* answer only from retrieved text, show source and section for every answer, and measure accuracy on the test questions.
2. **The checker wrongly blocks normal text:** papers about prompt injection quote attack examples, so legitimate content may be blocked. *Mitigation:* measure the false block rate and report it honestly.
3. **The checker misses attacks:** rule-based checks can be bypassed by rephrased instructions, which could give users false confidence. *Mitigation:* state the limitations clearly, don't claim full protection, and test with varied planted attacks.
4. **Copyright and misuse of the data:** copying papers into a public repo could breach licences. *Mitigation:* use open-access papers only, store links rather than PDFs, and keep all attack examples synthetic and in a local sandbox.
