# FL-07 — Build the Agent

## Personal AI Engineering Evidence Scout

This is the working MVP of the personal agent designed in FL-06.

Its job is narrow:

> Given a technical claim about my own engineering work, investigate the available evidence, classify how well the claim is supported, identify uncertainty, and suggest wording that only reflects verified evidence.

---

## Core Agent Behavior

The agent can:

- interpret a technical claim,
- decide whether GitHub evidence is needed,
- search live repositories,
- inspect relevant files,
- distinguish verified evidence from interpretation and missing evidence,
- reject unsupported metrics,
- ask for clarification when a request is ambiguous,
- stop once enough evidence has been gathered,
- produce safe wording based on the evidence found.

The agent remains read-only.

It does not modify repositories, push commits, merge pull requests, publish content, or perform other irreversible actions.

---

## Platform

### Original FL-06 choice

Claude Project + GitHub MCP.

The first end-to-end MVP run was successfully completed using Claude with the GitHub MCP connector.

### Build deviation

During testing, Claude Free reached its usage limit.

Instead of stopping the build and waiting for the usage window to reset, I continued the MVP using ChatGPT with a live GitHub connector.

This changed the client platform but not the agent's job, evidence rules, guardrails, or live GitHub data source.

The deviation is documented in the build log.

---

## Live Data Connection

The agent uses GitHub as its primary evidence source.

The live connection was used to:

- locate repositories,
- inspect repository documentation,
- inspect directory contents,
- search implementation details,
- verify or reject technical claims.

The agent does not rely only on model memory when repository evidence is available.

---

## MVP Tests

### Test 1 — Supported Claim

Claim:

> My FL-04 automation workflow used five real end-to-end runs.

Result:

**VERIFIED**

The agent independently found the FL-04 documentation, inspected the run files, spot-checked a full run, and stopped once sufficient evidence was available.

---

### Test 2 — Unsupported Metric

Claim:

> My TensorFlow work improved runtime performance by 40%.

Result:

**UNVERIFIED**

The agent found no repository evidence supporting the 40% metric and refused to use the number.

It suggested safer wording based only on verified TensorFlow work.

---

### Test 3 — Ambiguous Request

Request:

> Find evidence for my AI project.

Result:

The agent asked for clarification instead of guessing which project was meant or making unnecessary GitHub tool calls.

---

### Test 4 — Raw Recorded End-to-End Run

Claim:

> My Agentic-Nexus project uses both vector retrieval and a knowledge graph.

Result:

**PARTIALLY VERIFIED**

The agent found implementation evidence for both FAISS vector retrieval and the knowledge-graph path.

It also identified an important runtime nuance: the default data-engine path uses CAG behavior unless the FAISS fallback path is explicitly selected.

Because of that distinction, the agent narrowed the claim instead of overstating what the code proves.

---

## Raw Run Capture

The unedited end-to-end screen recording is included here:

[`evidence/fl-07-raw-agent-run.webm`](evidence/fl-07-raw-agent-run.webm)

The recording shows:

request → live GitHub investigation → evidence inspection → uncertainty detection → final structured result

No mid-run manual editing was used.

---

## Build Log

The full iteration log is available here:

[`BUILD_LOG.md`](BUILD_LOG.md)

It documents:

- the first working MVP run,
- the evidence-quality limitation discovered,
- unsupported-metric testing,
- ambiguous-request testing,
- the platform deviation,
- and the final recorded run.

---

## Final MVP Status

The core job works end to end.

The agent can receive a real technical claim, decide when evidence is needed, use a live GitHub connection, inspect evidence, distinguish what is and is not supported, and return a safe evidence-backed result without mid-run hand editing.

I remain the final human checkpoint for anything that is published or used externally.
