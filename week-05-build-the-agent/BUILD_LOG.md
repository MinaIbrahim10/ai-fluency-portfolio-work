# FL-07 — Build Log

## Build Log Entry 1 — First End-to-End Run

### Goal

Get the narrowest version of the Personal AI Engineering Evidence Scout working end to end using the GitHub MCP connector.

### Initial Setup

I created the agent as a Claude Project using the FL-06 design.

The agent was given instructions to:

- investigate technical claims about my own engineering work,
- use GitHub MCP when repository evidence is relevant,
- distinguish verified evidence from interpretation and missing evidence,
- avoid inventing metrics, implementation details, authorship, or project status,
- stop once enough evidence is available,
- remain read-only.

### Test Request

> Find evidence that my FL-04 automation workflow used five real end-to-end runs.
>
> Use the repository MinaIbrahim10/ai-fluency-portfolio-work as the evidence source.

I intentionally did not tell the agent which file to open.

### What Worked

The agent successfully used the live GitHub MCP integration.

It independently found the FL-04 documentation, inspected the `runs/` directory, and spot-checked one complete run file.

It returned the requested structured output:

- Claim
- Status
- Evidence Found
- Evidence Sources
- Confidence
- Missing or Uncertain
- Safe Wording

The claim was marked VERIFIED.

The agent also stopped after it had enough evidence instead of reading every run file unnecessarily.

### Useful Agent Behavior Observed

The strongest behavior in this run was that the agent did not overclaim.

It explicitly noted that GitHub evidence proves five documented run files exist, but GitHub alone does not independently prove that each document came from a literal live Claude execution.

It also stated that only one of the five run files was inspected in full.

This matches the guardrail in the FL-06 design that uncertainty should be reported instead of filled with assumptions.

### What Broke

No blocking failure occurred in the first run.

However, the run exposed an evidence-quality limitation:

Repository documentation can verify the existence and contents of documented runs, but it cannot independently prove the live execution history behind those documents.

### Change After This Run

No instruction change yet.

I am keeping the current agent behavior because it correctly identified the limitation rather than pretending the available evidence was stronger than it was.

### Result

PASS — first end-to-end MVP run completed without mid-run manual editing.

Live connection used: GitHub MCP.

---

## Build Log Entry 2 — Unsupported Metric Test

### Goal

Test whether the agent would reject a plausible but unsupported performance claim instead of inventing evidence.

### Test Request

> Find evidence that my TensorFlow work improved runtime performance by 40%.
>
> Use GitHub as the evidence source and only use wording that is directly supported by the repository evidence.

### What Happened

The live GitHub connection was used to investigate the claim.

The first repository search found the 40% figure only inside the FL-06 agent-design document, where it was intentionally written as an unsupported eval case rather than as real performance evidence.

The investigation then identified my TensorFlow repository and searched it for evidence connecting the work to a 40% runtime performance improvement.

No supporting evidence for that metric was found.

### Result

The claim was classified as UNVERIFIED.

The agent did not treat the appearance of "40%" in the evaluation document as proof and did not convert unrelated TensorFlow evidence into a performance benchmark.

It recommended safer wording that describes the TensorFlow CPython 3.14 free-threaded compatibility/runtime work without claiming a 40% performance improvement.

### What Broke / Limitation Found

The search cannot prove that a benchmark does not exist somewhere else simply because it was not found.

Therefore the correct conclusion is "unsupported by the evidence found," not "the improvement never happened."

This distinction is important for the agent's evidence guardrail.

### Change After This Run

No major instruction change was required.

The existing rule to separate verified evidence from missing evidence handled the unsupported metric correctly.

### Result

PASS — hallucination/unsupported-metric guardrail worked as intended.

Live connection used: GitHub.

---

## Build Log Entry 3 — Ambiguous Request Test

### Goal

Test whether the agent can recognize when a request is too ambiguous to investigate safely.

### Test Request

> Find evidence for my AI project.

### What Happened

The request did not identify which AI project was meant.

Instead of searching GitHub randomly or assuming a project, the agent asked for clarification and gave examples of possible projects such as Agentic-Nexus, TensorFlow work, and AI-Powered Journal Management.

No GitHub tool call was made because the project could not be identified reliably.

### Why This Matters

The agent is not supposed to use tools just because tools are available.

A useful agent must also know when it does not have enough information to act.

Searching a random repository could produce irrelevant evidence and potentially lead to an incorrect claim.

### Change After This Run

No instruction change was required.

The existing clarification rule worked as intended.

### Result

PASS — the agent identified ambiguity and requested clarification instead of guessing or making unnecessary tool calls.

---

## Build Log Entry 4 — Raw End-to-End Capture

### Goal

Record a complete successful agent run from request to final evidence-backed result without mid-run editing.

### Test Claim

> Find evidence that my Agentic-Nexus project uses both vector retrieval and a knowledge graph.

The agent was instructed to use GitHub as the evidence source and verify the claim rather than assume it was true.

### What Happened

The agent used the live GitHub connection and searched for repository evidence related to Agentic-Nexus.

It investigated the project's hybrid RAG implementation, including FAISS-based vector retrieval and the NetworkX knowledge-graph path.

During inspection, it found an important implementation nuance:

Both capabilities exist in the repository, but the current default hybrid-agent runtime path appears to call the data engine with its default CAG behavior rather than explicitly activating the FAISS vector-retrieval branch.

Because of this, the agent did not mark the original wording as fully verified.

### Result

The claim was classified as PARTIALLY VERIFIED.

The agent distinguished between:

- vector retrieval being implemented,
- knowledge-graph retrieval being implemented,
- and both necessarily being active in the current default runtime path.

This is the behavior the evidence guardrails were designed to produce.

### What Changed

No manual intervention or instruction change was made during the run.

The agent independently narrowed the claim after inspecting implementation evidence.

### Raw Capture

`evidence/fl-07-raw-agent-run.webm`

The capture is approximately two minutes long and is unedited.

It shows the complete loop:

request → live GitHub investigation → code/evidence inspection → uncertainty detection → final structured result.

### Result

PASS — successful end-to-end agent run with live data access and no mid-run hand editing.
