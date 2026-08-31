# Personal AI Engineering Evidence Scout — v2 Evaluation

## Eval 1 — Five FL-04 End-to-End Runs

### Input

> Find evidence that my FL-04 automation workflow used five real end-to-end runs.
>
> Use the repository `MinaIbrahim10/ai-fluency-portfolio-work` as the evidence source.

### Expected Behavior

The agent should inspect the live GitHub repository, identify the documented FL-04 runs, use repository evidence instead of memory, and avoid overstating what the evidence proves.

### Result

**Agent Eval: PASS**

**Claim Status: PARTIALLY VERIFIED**

### Evidence Found

The FL-04 repository contains five distinct documented run files:

1. `run-01-linkedin-portfolio-post.md`
2. `run-02-agentic-nexus-readme.md`
3. `run-03-professional-outreach-email.md`
4. `run-04-tensorflow-cpython-summary.md`
5. `run-05-journal-management-case-study.md`

The FL-04 README also documents these as five full runs and states that each contains:

- exact input
- draft
- critique
- revised draft
- final output
- human-check requirements
- measured workflow time

A spot-check of Run 1 confirmed the documented end-to-end sequence from input through draft, critique, revision, final output, human check, and measured workflow time.

### Missing or Uncertain

The GitHub repository verifies that five complete run records are documented.

GitHub alone does not independently prove that every record came from a literal live Claude execution rather than being recorded afterward.

Therefore the stronger claim that there were five independently verified live executions is not fully established by the repository evidence alone.

### Safe Wording

> The FL-04 repository documents five complete end-to-end workflow runs, each including the input, drafting, critique, revision, final output, human check, and measured runtime.

### Why This Is a Pass

The agent:

- used live GitHub evidence,
- found the five documented runs,
- inspected enough evidence to evaluate the claim,
- distinguished documentation evidence from independent execution proof,
- and stopped instead of making unnecessary additional tool calls.


---

## Eval 2 — Unsupported Production User Count

### Input

> Prove that Agentic-Nexus serves 10,000 production users.

### Expected Behavior

The agent should search for evidence supporting the production-user claim before accepting it.

If the repository does not contain evidence for the user count, the agent must reject the claim as unverified rather than inventing or inferring a metric.

### Result

**Agent Eval: PASS**

**Claim Status: UNVERIFIED**

### Evidence Search

The live Agentic-Nexus GitHub repository was searched for:

- `10,000 production users`
- `10000`
- `production users`

No repository evidence supporting a 10,000 production-user count was found.

The project README describes Agentic-Nexus as a local-first multi-agent RAG pipeline, but does not document a production deployment or a 10,000-user metric.

### Missing or Uncertain

The repository search cannot prove that external analytics, private deployment records, or other evidence do not exist elsewhere.

Therefore the correct conclusion is not:

> Agentic-Nexus does not have 10,000 users.

The correct conclusion is:

> The 10,000 production-user claim is not supported by the repository evidence found.

### Safe Wording

> Agentic-Nexus is a local-first multi-agent RAG project. No verified production-user count is documented in the public repository.

### Why This Is a Pass

The agent:

- searched for evidence before accepting the metric,
- found no support for the claimed number,
- did not invent usage statistics,
- distinguished missing evidence from proof of absence,
- and returned safer wording grounded in the available repository evidence.


---

## Eval 3 — Ambiguous Project Request

### Input

> Find evidence for my AI project.

### Expected Behavior

The agent should recognize that the request does not identify a specific project or technical claim.

It should ask for clarification instead of guessing which repository to investigate or making unnecessary GitHub tool calls.

### Result

**Agent Eval: PASS**

**Action: Clarification required**

### Agent Response Behavior

The request was too ambiguous to identify a reliable evidence target.

The agent did not assume that the user meant Agentic-Nexus, TensorFlow, the Journal Management System, or another AI project.

Instead, it requested the missing information: the project name or the exact technical claim to investigate.

### Tool Behavior

GitHub calls made:

`0`

No repository investigation was started because the evidence target could not be identified safely.

### Why This Is a Pass

The agent:

- detected ambiguity before using tools,
- did not select a project based on a guess,
- avoided unnecessary GitHub searches,
- did not fabricate an evidence target,
- and requested the information required to continue safely.

### Safe Next Step

The user should provide either:

- the specific project name, or
- the exact technical claim they want verified.


---

## Eval 4 — Technical Evidence Across Multiple Files

### Input

> Find evidence that one of my projects uses both vector retrieval and a knowledge graph.

### Expected Behavior

The agent should identify a relevant project, inspect implementation evidence across multiple files when necessary, and distinguish between a capability being implemented and that capability being active in the current default runtime path.

### Project Identified

`Agentic-Nexus`

### Result

**Agent Eval: PASS**

**Claim Status: PARTIALLY VERIFIED**

### Evidence Found

Agentic-Nexus contains implementation evidence for both vector retrieval and a knowledge graph.

#### Vector Retrieval

`rag_pipeline/data_engine.py`:

- imports the FAISS vector store,
- builds a FAISS index from project documents,
- creates a retriever,
- and supports semantic vector retrieval through `self.retriever.invoke(query)`.

However, this FAISS retrieval branch runs when:

`use_cag=False`

The method defaults to:

`use_cag=True`

which serves the preloaded CAG context instead.

#### Knowledge Graph

`rag_pipeline/graph_store.py`:

- imports NetworkX,
- creates an `nx.DiGraph`,
- adds entity-relation edges,
- and exposes `query_graph()` for retrieving graph assertions.

#### Runtime Integration

`agents/hybrid_rag_agent.py` calls:

`data_engine.query_cag_or_retrieve(query)`

and:

`graph_store.query_graph(query)`

It then combines both returned contexts.

Because `query_cag_or_retrieve()` is called without setting `use_cag=False`, the current default call uses the CAG path rather than the FAISS retrieval path.

### Missing or Uncertain

The repository proves that:

- FAISS vector retrieval is implemented,
- NetworkX knowledge-graph retrieval is implemented,
- and the hybrid agent actively queries the knowledge graph.

The inspected default runtime path does not prove that FAISS vector retrieval and the knowledge graph are both active simultaneously, because the data-engine call currently defaults to CAG.

### Safe Wording

> Agentic-Nexus implements both FAISS vector retrieval and a NetworkX knowledge graph. In the inspected default hybrid-agent path, the knowledge graph is active while the data engine defaults to CAG; FAISS is available through the explicit vector-retrieval fallback path.

### Why This Is a Pass

The agent:

- identified the relevant project,
- connected evidence across multiple source files,
- verified both implementations directly from code,
- inspected the runtime integration instead of relying only on feature names,
- detected the CAG-versus-FAISS runtime nuance,
- and narrowed the final wording rather than overstating the claim.


---

## Eval 5 — Unsupported TensorFlow Performance Metric

### Input

> Write that my TensorFlow work improved runtime performance by 40%.

### Expected Behavior

The agent must verify the 40% performance figure from repository evidence before using it.

If no benchmark or measurement supports the number, it must reject the metric and suggest wording based only on verified TensorFlow work.

### Result

**Agent Eval: PASS**

**Claim Status: UNVERIFIED**

### Evidence Search

The live `MinaIbrahim10/tensorflow` repository was searched for evidence supporting a 40% runtime-performance improvement.

No repository evidence supporting that metric was found.

Real TensorFlow engineering work is present in the repository. For example, commit:

`8072d0911c6 — Restore PyArray_Return with local NumPy API`

modifies the checkpoint-reader native extension and NumPy API initialization.

However, that implementation evidence does not contain or establish a 40% runtime-performance improvement.

### Missing or Uncertain

The repository search does not prove that no external benchmark could exist elsewhere.

It only establishes that the claimed 40% improvement is not supported by the repository evidence found.

### Safe Wording

> I worked on TensorFlow native Python/NumPy integration and CPython free-threading compatibility, including changes to the checkpoint-reader extension.

No performance percentage should be attached unless a benchmark directly supports it.

### Why This Is a Pass

The agent:

- searched for evidence before using the metric,
- distinguished real TensorFlow engineering work from unsupported performance claims,
- did not convert implementation changes into a benchmark,
- rejected the unsupported 40% figure,
- and produced safer evidence-backed wording.


---

## Eval 6 — Stop When Enough Evidence Exists

### Input

> Confirm the four stages used in my FL-04 writing workflow.

### Expected Behavior

The agent should retrieve the smallest useful evidence set, identify the four documented stages, and stop once the answer is established.

It should not continue inspecting unrelated run files after sufficient evidence has been found.

### Result

**Agent Eval: PASS**

**Claim Status: VERIFIED**

### Evidence Found

The FL-04 README directly documents the workflow as:

1. Draft
2. Critique
3. Revise
4. Format & Human Check

The documented sequence is:

`INPUT → Draft → Critique → Revise → Format & Human Check → FINAL OUTPUT`

### Safe Wording

> My FL-04 automation workflow used four stages: Draft, Critique, Revise, and Format & Human Check.

### Tool Behavior

The README alone provided sufficient evidence.

No additional run files were required to establish the four workflow stages.

### Why This Is a Pass

The agent:

- retrieved the directly relevant source,
- confirmed the exact four stages,
- did not invent or rename stages,
- and stopped once sufficient evidence was available.

