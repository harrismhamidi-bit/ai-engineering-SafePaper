# SafePaper: A Research Paper Assistant with Prompt-Injection Screening

> Answers questions about LLM agent security research papers, grounded in
> open-access sources, and screens retrieved text for hidden instructions
> before the AI reads it.

## Problem Statement
Students doing literature reviews must read many long, dense papers to find
a single method, dataset or result. An AI assistant can speed this up, but
any assistant that reads outside documents can be tricked by instructions
hidden inside them (indirect prompt injection). SafePaper gives sourced
answers from a small set of papers while checking each retrieved passage
before use.

## Evidence of the Problem
- Key information in a literature review is spread across multiple papers,
  so one question may need several sources.
- Indirect prompt injection is a documented risk for AI systems that read
  external content (see OWASP Top 10 for LLM Applications).

## Initial Related Work / Existing Approaches
- Manual reading and keyword search in PDFs: reliable, but slow and cannot
  combine answers across papers.
- General-purpose AI assistants: flexible, but answers may not be grounded
  in the chosen papers and cite no sources.
- Basic RAG assistants: grounded in documents, but usually trust all
  retrieved text without checking it.

## Engineering Gap / Limitation
Basic document Q&A systems pass retrieved text straight to the model, so a
planted instruction in a document can change the assistant's behaviour.
This project adds a lightweight screening step and measures how much
security it adds, and at what cost to answer quality and speed.

## Project Objectives
- O1: Design a document-grounded Q&A assistant over 3 open-access papers.
- O2: Develop it with retrieval and a rule-based safety checker, with an
  optional small local validator model.
- O3: Evaluate answer accuracy, attack blocking rate, false blocks and
  latency.

## Target Users
Undergraduate students doing literature reviews on LLM agent security.

## Data Sources
- Paper 1: [title, authors, year, link]
- Paper 2: [title, authors, year, link]
- Paper 3: [title, authors, year, link]

PDFs are not stored in this repository. All attack examples are synthetic.

## Risk Statement
Information-only assistant. It gives no medical, legal or mental health
advice and makes no autonomous decisions. Attack tests run only on local
copies of the papers.

## Weekly Progress
| Week | Focus | Deliverable | Status |
|------|-------|-------------|--------|
| W1 | System map + project scope | README + docs | ✅ |
