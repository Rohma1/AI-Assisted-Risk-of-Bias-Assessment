# AI-Assisted Risk of Bias Assessment

A small prototype of an **AI-assisted Risk of Bias module** for an AI-powered systematic review platform.

The prototype demonstrates how research papers can be processed, relevant evidence can be retrieved for Risk of Bias questions, and structured assessments can be stored for later algorithm-based judgment.

## Overview

The system is designed around the **Cochrane Risk of Bias 2 (RoB 2)** framework for randomized trials.

RoB 2 assesses a specific result from a randomized trial across **5 mandatory bias domains**:

1. Bias arising from the randomization process
2. Bias due to deviations from intended interventions
3. Bias due to missing outcome data
4. Bias in measurement of the outcome
5. Bias in selection of the reported result

Each domain uses signalling questions. Answers to these questions are mapped by the RoB 2 methodology to a proposed domain-level judgment:

* Low risk of bias
* Some concerns
* High risk of bias

The assessment is result-specific rather than simply assigning one risk score to an entire paper.

## Current Prototype

The current Colab prototype implements the initial components of the planned module:

```text
Research Papers
      ↓
PDF Extraction
      ↓
Page-aware Text
      ↓
Text Chunking
      ↓
Sentence Embeddings
      ↓
FAISS Retrieval
      ↓
Relevant Evidence
      ↓
RoB 2 Assessment Structure
```

### Current features

* Upload multiple PDF research papers
* Extract text using PyMuPDF
* Preserve page numbers for evidence tracing
* Split extracted text into searchable chunks
* Generate embeddings using `all-MiniLM-L6-v2`
* Store embeddings in a FAISS similarity index
* Retrieve evidence relevant to a Risk of Bias question
* Restrict retrieval to a selected paper
* Create a structured RoB 2 assessment object
* Represent the 5 RoB 2 domains
* Store signalling questions, judgments and justifications

## Technologies

| Component         | Technology                        |
| ----------------- | --------------------------------- |
| Development       | Google Colab                      |
| Language          | Python                            |
| PDF extraction    | PyMuPDF                           |
| Embeddings        | Sentence Transformers             |
| Embedding model   | `all-MiniLM-L6-v2`                |
| Vector search     | FAISS                             |
| Data handling     | Pandas                            |
| Planned interface | Gradio                            |
| Planned LLM       | Small Hugging Face instruct model |
| GPU               | NVIDIA Tesla T4                   |

## Example Workflow

For a paper, the system can retrieve evidence for a question such as:

```text
Was the allocation sequence random?
```

The retrieval system searches the selected paper and returns relevant passages together with their page numbers.

Example:

```text
Question:
Was the allocation sequence random?

Evidence:
Page 3

Participants were randomly allocated to three
parallel study groups...
```

The planned AI-assisted workflow is:

```text
RoB 2 Question
      ↓
Evidence Retrieval
      ↓
Relevant Paper Passages
      ↓
Small LLM
      ↓
Suggested Answer
      ↓
Researcher Review
      ↓
Final Signalling Answer
      ↓
RoB 2 Decision Algorithm
      ↓
Domain Judgment
```

The LLM is intended to **assist the researcher**, not replace the Risk of Bias methodology or the researcher's final judgment.

## Planned Development

The current prototype is an initial implementation. The next stages are:

### Phase 1 — RoB 2 Engine

Implement the complete RoB 2 signalling-question structure and official decision logic for all 5 domains.

### Phase 2 — AI Evidence Assistant

Use a small Hugging Face instruct model to:

* interpret retrieved evidence
* suggest answers to signalling questions
* provide supporting explanations
* identify relevant page numbers
* distinguish evidence from uncertainty

### Phase 3 — Researcher Verification

Allow the researcher to:

* accept the AI suggestion
* change the answer
* add a justification
* review the supporting evidence
* override the proposed judgment when appropriate

### Phase 4 — Complete Five-Domain Assessment

Implement:

```text
Domain 1 → Randomization
Domain 2 → Deviations from intended interventions
Domain 3 → Missing outcome data
Domain 4 → Measurement of outcome
Domain 5 → Selection of reported result
```

### Phase 5 — Multi-Paper Assessment

Test the module on approximately **5–6 randomized trials** and generate a Risk of Bias summary table.

### Phase 6 — Web Application

Move the prototype architecture into the main systematic-review platform.

## Important Design Principle

The system separates **AI interpretation** from **framework decision logic**.

```text
AI / RAG
  ↓
Find and interpret evidence
  ↓
Suggest signalling answer

RoB 2 Engine
  ↓
Apply framework rules
  ↓
Propose risk-of-bias judgment

Researcher
  ↓
Review and confirm
```

This prevents the LLM from inventing its own Risk of Bias methodology.

## Prototype Status

**Current status:** Early prototype / proof of concept.

The current implementation demonstrates the evidence-retrieval foundation and RoB 2 data structure. The complete five-domain algorithm and AI-assisted assessment are planned for subsequent development.

## Purpose

This prototype is part of a larger **AI-Powered Systematic Review & Literature Review Platform** intended to assist researchers throughout the systematic review workflow, including literature screening, Risk of Bias assessment, data extraction and evidence synthesis.
# AI-Assisted-Risk-of-Bias-Assessment
