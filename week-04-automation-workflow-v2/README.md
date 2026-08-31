# Week 4 — Ship an Automation Workflow v2

General AI Fluency — Build (Core)

Assignment code: FL-04

## Workflow

I built a no-code writing workflow inside a Claude Project.

The workflow is:

INPUT
↓
STAGE 1 — Draft
↓
STAGE 2 — Critique
↓
STAGE 3 — Revise
↓
STAGE 4 — Format & Human Check
↓
FINAL OUTPUT

---

# 1. Workflow Design

## Stage 1 — Draft

Input:
- raw user request
- audience
- goal
- requested format
- constraints
- factual inputs

Action:
Create a first draft using only the supplied information.

Output:
The draft is passed to Stage 2.

---

## Stage 2 — Critique

Input:
Stage 1 draft.

Action:
Review the draft for:

- goal alignment
- audience fit
- clarity
- tone
- concision
- unsupported claims
- vague language
- missing evidence
- unnecessary repetition

Output:
The original draft plus a structured critique are passed to Stage 3.

---

## Stage 3 — Revise

Input:
Draft + critique.

Action:
Rewrite the draft to fix the identified problems.

This is not only a copy-editing step. The workflow is instructed to remove or correct unsupported claims and improve the structure.

Output:
Revised draft passed to Stage 4.

---

## Stage 4 — Format & Human Check

Input:
Revised draft.

Action:
Format the result for the requested destination, such as:

- LinkedIn
- GitHub README
- professional email
- technical portfolio summary
- portfolio case study

Then create a Human Check list.

Output:
Final formatted result + verification checklist.

---

# 2. Claude Project Configuration

The Claude Project instructions require all four stages to run in order.

Core rules:

1. Always show all four stages.
2. Keep stages separate.
3. Never invent missing facts.
4. Flag missing information.
5. Preserve technical terminology.
6. Produce a usable final result.
7. Require human review before publishing.
8. Treat each new input as a fresh workflow run.

---

# 3. Five Real Runs

## Run 1 — LinkedIn Portfolio Post

Audience:
Technical recruiters and AI engineering hiring managers.

Goal:
Create a concise LinkedIn post announcing my AI engineering portfolio.

Input included:

- Generative AI
- LLMs
- RAG / agentic AI
- TensorFlow open-source work
- production systems
- portfolio URL
- Agentic-Nexus details

Workflow result:

The first draft was reviewed and shortened.

The critique identified:

- unnecessary interpretation
- possible redundancy
- claims that needed tighter phrasing
- word-count risk

The final output was reduced to approximately 102 words.

### Time

17 seconds.

---

## Run 2 — Agentic-Nexus README

Audience:
A hiring manager reviewing my GitHub profile.

Goal:
Create a concise README project overview.

Input included:

- multi-agent orchestration
- Hybrid RAG
- vector retrieval
- knowledge graphs
- tool use
- coding workflows
- automated evaluation

Workflow result:

The critique identified an unsupported comparison that implied Hybrid RAG provided "more structured" retrieval than vector search alone.

That claim was removed.

The final README kept only supplied technical facts and added a "What to inspect" section.

### Time

18 seconds.

---

## Run 3 — Professional Outreach Email

Audience:
Technical hiring manager.

Goal:
Write a professional email asking about relevant AI engineering opportunities.

Input included:

- Generative AI
- LLMs
- agentic AI
- backend engineering
- TensorFlow open-source work
- portfolio URL

Workflow result:

The critique identified:

- information carried over from previous context that was not explicitly supplied in this run
- unsupported use of the word "research"
- missing recipient/name placeholders that required human completion

These were corrected or flagged.

### Time

21 seconds.

---

## Run 4 — TensorFlow / CPython Technical Summary

Audience:
Software engineers and ML engineers.

Goal:
Write a technical portfolio summary of TensorFlow / CPython 3.14 free-threading work.

Input included:

- CPython 3.14t
- TensorFlow
- GIL behavior
- native synchronization
- Python object ownership
- pybind11
- ABI handling
- runtime compatibility
- 800 concurrent TensorFlow operation batches
- 800 synchronous gRPC RPCs
- 500 asynchronous gRPC RPCs
- 12 merged TensorFlow PRs

Workflow result:

The critique identified:

- interpretive language beyond the supplied facts
- a causal claim about PRs
- language that implied a test purpose not explicitly given
- word-count overflow

The final version was reduced to approximately 195 words and kept the factual claims conservative.

### Time

27 seconds.

---

## Run 5 — AI-Powered Journal Management Case Study

Audience:
Technical recruiters, AI engineers, and engineering managers.

Goal:
Create a concise portfolio case-study summary.

Input included:

- submission screening
- NLP classification
- reviewer matching
- citation analysis
- plagiarism signals
- summarization
- editorial workflows
- FastAPI backend

Workflow result:

The critique identified:

- unsupported generalizations about manual journal workflows
- wording that implied stronger system integration than the supplied facts confirmed
- missing technical proof for specific NLP methods
- unknown deployment status

The final case study retained only supported claims and explicitly listed evidence that still needs to be verified.

### Time

23 seconds.

---

# 4. Timing

Workflow times:

| Run | Task | Time |
|---|---|---:|
| 1 | LinkedIn portfolio post | 17 sec |
| 2 | Agentic-Nexus README | 18 sec |
| 3 | Professional outreach email | 21 sec |
| 4 | TensorFlow technical summary | 27 sec |
| 5 | Journal Management case study | 23 sec |

Total workflow time:

106 seconds.

Average workflow time:

21.2 seconds per task.

---

# 5. Manual Baseline

I manually completed the same type of professional outreach email task used in Run 3.

Manual time:

2 minutes 51 seconds = 171 seconds.

The manual draft was written without AI assistance.

It included the core message, but compared with the workflow output it required additional cleanup for:

- grammar
- spelling
- sentence structure
- claim precision
- proof linking
- tone
- formatting

---

# 6. Time Saved Estimate

Manual baseline:

171 seconds.

Workflow average:

21.2 seconds.

Estimated time saved per comparable task:

149.8 seconds.

That is approximately:

2 minutes 30 seconds saved per task.

Approximate reduction:

87.6% less time for the workflow execution itself.

This comparison does not include the initial setup time for building the Claude Project workflow.

---

# 7. Setup Cost

The workflow was not free in time to create.

Setup included:

- designing the four stages
- writing structured Project Instructions
- defining handoffs
- testing the workflow
- running five real examples
- adjusting expectations around factual verification

The setup cost is therefore front-loaded.

The value appears when the same workflow is reused across many future writing tasks.

---

# 8. Failure Points

The workflow still has several failure modes.

## Unsupported Interpretation

The model may add reasonable-sounding interpretation beyond the input facts.

Examples found during testing:

- explaining why a technical test was performed
- making comparative claims about retrieval methods
- describing a system as fully integrated without enough evidence

Human review is required.

---

## Context Leakage

The model may reuse facts from earlier messages that were not explicitly provided in the current run.

This happened during the professional email test.

The critique stage caught it, but the human still needs to verify the final output.

---

## Technical Precision

The model can simplify a technical mechanism in a way that is understandable but not perfectly precise.

Examples:

- synchronization details
- reviewer matching logic
- Hybrid RAG behavior
- plagiarism detection method
- ABI / runtime descriptions

Technical claims must be checked against the actual implementation.

---

## Changing Facts

Some facts may become outdated.

Examples:

- number of merged pull requests
- deployment status
- project capabilities
- repository structure
- live URLs

These must be checked before publishing.

---

## Missing Evidence

The workflow can produce a polished description even when the evidence is incomplete.

It must not be treated as proof.

Examples still requiring human verification can include:

- benchmarks
- metrics
- production scale
- users
- deployment status
- exact models
- implementation details

---

# 9. Required Human Review

Before publishing or sending any final output, a human must verify:

- names
- dates
- links
- metrics
- technical claims
- project status
- attribution
- organizational context
- confidential information
- tone
- whether claims have supporting evidence

The workflow improves writing quality, but it does not replace factual responsibility.

---

# 10. End-to-End Test

The workflow was tested on five different real inputs:

- social media writing
- GitHub documentation
- professional outreach
- technical portfolio writing
- case-study writing

Each run successfully moved through:

Draft
→ Critique
→ Revise
→ Format
→ Human Check

This demonstrates that the workflow can handle a new input without needing to redesign the process.

---

# Final Assessment

The workflow is useful because it separates generation from review.

A single prompt can create a draft quickly, but this workflow adds:

- structured critique
- revision
- output formatting
- factual caution
- mandatory human verification

The main benefit is not just speed.

It is consistency and a more reliable review process across different types of writing.
