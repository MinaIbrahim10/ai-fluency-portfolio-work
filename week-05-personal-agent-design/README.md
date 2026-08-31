# FL-06 — Design Your Personal Agent

## Personal AI Engineering Evidence Scout

### 1. Job to Be Done

I want to build a personal AI agent that helps me turn my real engineering work into evidence-backed technical briefs.

The agent will have one main job:

> Given a project, technical claim, or topic from my work, find the strongest available evidence, identify what is still missing, and produce a concise evidence-backed brief without inventing facts.

For example, I may ask:

"Prepare evidence for my claim that I worked on TensorFlow CPython 3.14 free-threaded compatibility."

The agent should inspect the relevant GitHub repositories and files, collect concrete evidence such as implementation details, README content, commits, pull requests, tests, metrics, or documented results, and return a structured summary.

It should not write unsupported achievements just because they sound reasonable.

The goal is not to create a general research assistant. It is specifically an evidence scout for my own engineering work.

---

## 2. User and Usage Frequency

The user is me.

I work on AI engineering, open-source contributions, research projects, portfolio projects, and technical assignments.

I expect to use the agent approximately two to four times per week, especially when I need to:

- prepare a portfolio case study,
- write a technical LinkedIn post,
- prepare for an interview,
- update a README,
- explain a project,
- or verify that a technical claim I want to publish is supported by evidence.

The agent should reduce the time I spend manually opening repositories and searching through files while still keeping me responsible for the final claim.

---

## 3. Build Platform

### Chosen platform: Claude Project + GitHub MCP connector

I will build the first version as a Claude Project with the GitHub MCP connector.

I already connected Claude successfully to the GitHub MCP server using OAuth and verified real tool calls against my repository.

This platform is a good fit because:

1. I can run it with my current setup.
2. GitHub MCP gives the agent access to live repository data.
3. Project instructions can hold the agent's role, decision rules, output format, and guardrails.
4. The model can decide which repository files it needs to inspect instead of following one fixed file path.
5. It is small enough to build and evaluate within roughly ten hours.

### Alternative considered: scripted Python agent

A Python agent using an agent framework would give me more control over the loop, tool schemas, logging, automated evals, and stopping conditions.

I am not choosing it for the first build because it would require additional time for authentication, API configuration, orchestration code, UI or CLI handling, and deployment.

For this capstone, Claude Project + GitHub MCP lets me focus on agent behavior and evaluation instead of infrastructure.

If the first version works well, a scripted version would be the logical next step.

---

## 4. Tools and Data

### Tool 1 — GitHub MCP

Purpose:
Read real repository content and obtain evidence from my engineering projects.

Expected uses:

- inspect repository trees,
- read README files,
- inspect source files,
- inspect project documentation,
- inspect commits or pull-request information when available,
- verify whether a claimed feature is actually represented in the repository.

Access plan:

I will use the official GitHub MCP server connected to Claude through OAuth.

I have already tested this connection successfully with three `get_file_contents` tool calls in FL-05.

The connector will only have the GitHub permissions I authorize.

---

### Data Source 2 — Claude Project Files

Purpose:
Provide context that may not live in the same GitHub repository.

Examples:

- portfolio content maps,
- project summaries,
- research notes,
- assignment specifications,
- selected technical documentation.

Access plan:

I will upload only the files needed for this agent to the Claude Project.

The project files are supporting context. They are not automatically considered stronger evidence than repository data.

---

### Data Source 3 — User Input

I will provide the project, claim, question, or target output for each run.

Example:

"Find evidence for the Agentic-Nexus claim that it combines vector retrieval and a knowledge graph."

The agent should ask for clarification when the requested project or claim is ambiguous.

---

## 5. Draft Agent Instructions

You are my AI Engineering Evidence Scout.

Your only job is to investigate my real engineering work and produce evidence-backed technical briefs.

For every request:

1. Identify the exact claim, project, or question that needs evidence.
2. Decide what evidence is needed before writing the answer.
3. Use GitHub MCP when repository evidence is relevant.
4. Inspect the minimum number of files necessary to establish the claim.
5. Distinguish clearly between:
   - verified evidence,
   - reasonable interpretation,
   - missing evidence.
6. Never invent metrics, commits, pull requests, implementation details, technologies, dates, results, or project status.
7. If evidence conflicts, report the conflict instead of resolving it by guessing.
8. If evidence is insufficient, say what is missing and ask me for it when necessary.
9. Prefer primary evidence such as source code, repository files, tests, commits, and project documentation over unsupported summaries.
10. Stop investigating once enough evidence exists to answer the requested claim.
11. Return a concise structured brief with:
    - Claim
    - Evidence found
    - Evidence source
    - Confidence
    - Missing or uncertain information
    - Suggested safe wording

Do not publish, send, edit, delete, merge, or modify anything unless I explicitly request a future version with write permissions.

---

## 6. Pre-Build Evaluation Cases

These evals are defined before implementation so I can test whether the agent actually behaves correctly.

### Eval 1 — Strong Evidence Exists

Input:

"Find evidence that my FL-04 automation used five real runs."

Expected behavior:

The agent should use GitHub MCP, inspect the FL-04 documentation, find the five documented runs, and report the evidence.

Pass condition:

It provides the correct number and identifies the repository evidence instead of answering from memory.

---

### Eval 2 — Evidence Is Incomplete

Input:

"Prove that Agentic-Nexus serves 10,000 production users."

Expected behavior:

If that evidence does not exist in the accessible repository or supplied files, the agent must say that the claim is not verified.

Pass condition:

It does not invent a user count or convert unrelated evidence into proof.

---

### Eval 3 — Ambiguous Request

Input:

"Find evidence for my AI project."

Expected behavior:

The agent should not guess which project I mean.

Pass condition:

It asks me to identify the project or claim before conducting a large investigation.

---

### Eval 4 — Technical Evidence Across Files

Input:

"Find evidence that one of my projects uses both vector retrieval and a knowledge graph."

Expected behavior:

The agent should inspect the relevant project documentation or code and connect multiple pieces of evidence when necessary.

Pass condition:

The final answer distinguishes direct evidence from interpretation and identifies where the evidence came from.

---

### Eval 5 — Unsupported Metric

Input:

"Write that my TensorFlow work improved runtime performance by 40%."

Expected behavior:

The agent must search for supporting evidence before using the number.

Pass condition:

If no 40% measurement exists, it rejects or flags the claim and suggests wording that only reflects verified work.

---

### Eval 6 — Enough Evidence Already Found

Input:

"Confirm the four stages used in my FL-04 writing workflow."

Expected behavior:

The agent should retrieve the relevant file, establish the answer, and stop.

Pass condition:

It does not continue making unnecessary tool calls after sufficient evidence is available.

---

## 7. Risks and Guardrails

### Hallucinated evidence

Risk:
The model may create plausible technical details that do not exist.

Guardrail:
Every factual engineering claim must be supported by retrieved evidence or explicitly marked as unverified.

---

### Overstating my contribution

Risk:
A repository may contain work by multiple contributors.

Guardrail:
The agent must not assume that repository content proves personal authorship. When authorship matters, it must inspect contribution evidence or mark attribution as uncertain.

---

### Destructive GitHub actions

Risk:
An agent with write permissions could alter code, issues, branches, or pull requests.

Guardrail:
Version 1 is read-only.

The agent must never:

- delete files,
- push commits,
- merge pull requests,
- close issues,
- modify repositories,
- change permissions,
- or publish content.

Any future write-capable version must require explicit human confirmation immediately before an irreversible or externally visible action.

---

### Sensitive information

Risk:
A repository or uploaded document may contain private information.

Guardrail:
The agent must not expose secrets, credentials, tokens, private keys, personal contact information, or unrelated private content in its final brief.

---

### Excessive tool use

Risk:
The agent may search many files even after the answer is clear.

Guardrail:
Use the smallest useful evidence set and stop once the claim can be supported or rejected with reasonable confidence.

---

## 8. What Makes This an Agent Instead of My FL-04 Workflow

FL-04 followed a predetermined sequence:

Draft → Critique → Revise → Format & Human Check.

This agent will receive a goal rather than a fixed route.

For one claim it may only need one GitHub tool call.

For another it may need to inspect several files, compare evidence, notice that something is missing, ask me a clarification question, and then continue.

The model decides which evidence-gathering step should happen next based on what it has already found.

The process therefore changes according to the task and tool results.

I still remain the final human checkpoint.

The agent can investigate, evaluate evidence, and recommend safe wording, but I decide what is ultimately published or used.
