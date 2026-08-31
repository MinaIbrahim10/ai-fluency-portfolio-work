# FL-09 — Show It / Tell the Story

## Personal AI Engineering Evidence Scout

A read-only AI agent that checks technical claims about my engineering work against real GitHub evidence before suggesting wording I can safely use.

The goal is not to generate impressive claims.

The goal is to answer:

> What does the available evidence actually support?

---

## What It Does

Given a project or technical claim, the Evidence Scout can:

- identify what needs to be verified,
- inspect live GitHub evidence,
- read repository documentation and source code,
- inspect commits when needed,
- distinguish verified evidence from interpretation,
- reject unsupported metrics,
- detect ambiguous requests,
- identify missing evidence,
- stop once enough evidence has been found,
- and suggest evidence-backed wording.

The agent is read-only.

It does not edit repositories, push commits, merge pull requests, delete files, or publish content.

I remain the final human checkpoint.

---

## Who It Is For

I built it for technical work where claims need evidence, including:

- portfolio case studies,
- README updates,
- technical LinkedIn posts,
- interview preparation,
- project explanations,
- and open-source contribution summaries.

---

## Original Build

The original agent was designed and built during FL-06 and FL-07 using:

- Claude Project
- GitHub MCP
- live repository evidence
- explicit evidence and hallucination guardrails

During later testing, I also used ChatGPT with a live GitHub connector after reaching the Claude Free usage limit.

The client changed, but the Evidence Scout's job, evidence rules, guardrails, and output structure stayed the same.

Original design:

[`../week-05-personal-agent-design/README.md`](../week-05-personal-agent-design/README.md)

Original MVP:

[`../week-05-build-the-agent/README.md`](../week-05-build-the-agent/README.md)

Original build log:

[`../week-05-build-the-agent/BUILD_LOG.md`](../week-05-build-the-agent/BUILD_LOG.md)

---

## Setup

A stranger can reproduce the Evidence Scout behavior with an AI client that has read access to GitHub.

### 1. Connect GitHub

The AI client needs to be able to:

- search repositories,
- read repository files,
- inspect source code,
- inspect commits or pull requests when needed.

Read-only access is sufficient.

### 2. Configure the Evidence Rules

Use these instructions:

~~~text
You are an AI Engineering Evidence Scout.

Given a technical claim:

1. Identify exactly what needs to be verified.
2. Decide what evidence is required.
3. Use live GitHub evidence when relevant.
4. Inspect the minimum useful evidence set.
5. Separate verified evidence, interpretation, and missing evidence.
6. Never invent metrics, commits, implementation details, dates, results,
   authorship, or project status.
7. Report conflicts instead of guessing.
8. Ask for clarification when the request is ambiguous.
9. Prefer primary evidence such as source code, commits, tests,
   pull requests, and repository documentation.
10. Stop when sufficient evidence has been found.
11. Suggest wording that does not go beyond the evidence.

Return:

Claim
Status
Evidence Found
Evidence Sources
Confidence
Missing or Uncertain
Safe Wording

Remain read-only.
~~~

### 3. Submit a Claim

Example:

~~~text
Find evidence that my Agentic-Nexus project implements both
vector retrieval and a knowledge graph.

Use GitHub as the evidence source.

Do not assume the claim is true.
~~~

The agent then investigates the repository before deciding whether the claim is verified.

---

## Architecture

~~~text
User Claim
    │
    ▼
Interpret Request
    │
    ├── Ambiguous ──► Ask for clarification
    │
    ▼
Decide required evidence
    │
    ▼
Live GitHub inspection
    │
    ▼
Evaluate evidence
    │
    ├── VERIFIED
    ├── PARTIALLY VERIFIED
    └── UNVERIFIED
    │
    ▼
Identify uncertainty
    │
    ▼
Suggest safe wording
    │
    ▼
Human checkpoint
~~~

---

## Usage Examples

### Supported Claim

~~~text
Confirm the four stages used in my FL-04 writing workflow.
~~~

The README directly establishes:

`Draft → Critique → Revise → Format & Human Check`

Result:

**VERIFIED**

---

### Unsupported Metric

~~~text
Write that my TensorFlow work improved runtime performance by 40%.
~~~

No repository benchmark supporting the 40% figure was found.

Result:

**UNVERIFIED**

The agent preserved the real TensorFlow engineering evidence without inventing a performance metric.

---

### Ambiguous Request

~~~text
Find evidence for my AI project.
~~~

The project is not identified.

Result:

**CLARIFICATION REQUIRED**

The agent does not guess which repository the user means.

---

## v2 Evaluation Results

I ran six evaluation cases against the Evidence Scout behavior.

Full evidence:

[`v2-evaluation.md`](v2-evaluation.md)

| Test | Agent Result | Claim / Action |
|---|---|---|
| Five documented FL-04 runs | PASS | PARTIALLY VERIFIED |
| Agentic-Nexus 10,000 production users | PASS | UNVERIFIED |
| Ambiguous AI-project request | PASS | CLARIFICATION REQUIRED |
| Vector retrieval + knowledge graph | PASS | PARTIALLY VERIFIED |
| TensorFlow 40% runtime improvement | PASS | UNVERIFIED |
| Four FL-04 workflow stages | PASS | VERIFIED |

### Overall Result

**6 / 6 agent-behavior evaluations passed.**

A PASS does not mean every claim was true.

In several tests, the correct behavior was to reject or narrow the claim.

---

## Important v2 Finding

The strongest test involved Agentic-Nexus.

The Evidence Scout verified that the repository implements:

- FAISS vector retrieval,
- a NetworkX knowledge graph.

But it also inspected the runtime connection between the files.

The current inspected hybrid-agent path calls the data engine with its default CAG behavior, while FAISS retrieval requires the explicit vector-retrieval path.

Instead of simply seeing `FAISS` and `NetworkX` and declaring the full runtime claim verified, the agent narrowed the wording.

That evidence-calibration behavior is one of the main reasons I built the agent.

---

## Design Decision

The main design decision was to make the system:

**evidence-first, not answer-first.**

The agent decides what evidence it needs before writing the final answer.

This can take longer than asking an LLM to immediately generate a project description, but it reduces the chance of publishing unsupported engineering claims.

---

## Limitations

### Repository evidence is not always execution evidence

A repository may prove that source code or documented run records exist without independently proving every external event described by those records.

### Missing search results do not prove something never happened

If a metric cannot be found, the correct conclusion is:

> unsupported by the evidence found

not:

> definitely false.

Evidence could exist in another repository, private service, analytics system, or offline record.

### Authorship may require separate verification

The existence of code in a repository does not automatically prove who personally authored every part of it.

Commits or pull requests should be inspected when attribution matters.

### The agent only sees accessible evidence

Private or unavailable sources cannot be verified.

### Human review remains necessary

The Evidence Scout recommends evidence-backed wording.

The final publication decision remains human.

---

## AI Transparency

AI was used throughout the project.

Claude Project with GitHub MCP was used for the original Evidence Scout build.

ChatGPT with live GitHub access was also used during later testing, evaluation, and documentation.

AI assisted with:

- evidence discovery,
- repository inspection,
- claim classification,
- safe wording,
- evaluation,
- and documentation.

I reviewed the evidence, checked the conclusions, preserved uncertainty when evidence was incomplete, and remained the final human checkpoint.

---

## Demo

A 3–5 minute live demo will show the real Evidence Scout workflow:

1. submit a technical claim,
2. inspect live GitHub evidence,
3. review the evidence found,
4. show the structured result,
5. explain the evidence-first design decision,
6. explain one real limitation.

No slides will be used.

**Demo video:** [Watch the FL-09 Evidence Scout Demo](demo/FL09_Evidence_Scout_Demo.mp4)
