# Design Decisions

## 1. Project Objective

The objective was to build an autonomous AI research agent capable of planning research tasks, collecting information from multiple sources, analyzing findings, and generating structured research reports with minimal manual intervention.

## 2. Technology Selection

### n8n – Workflow Orchestration

**Decision:** n8n was selected as the central automation platform.

**Reason:**
- Provides visual workflow orchestration.
- Supports API integrations and custom JavaScript.
- Makes multi-step automation easier to maintain.
- Allows individual workflow stages to be tested and modified.

### Ollama – Local LLM Inference

**Decision:** Ollama was selected to run the language model locally.

**Reason:**
- Provides access to locally hosted language models.
- Reduces dependence on paid LLM inference APIs.
- Supports HTTP-based integration with n8n.
- Offers control over model selection and generation settings.

**Selected model:** Qwen 3 1.7B.

### Tavily – Web Search and Extraction

**Decision:** Tavily was selected for web search and webpage extraction.

**Reason:**
- Provides research-oriented search results.
- Supports extracting relevant webpage content.
- Helps the agent gather information from external websites.

### Wikipedia – Additional Knowledge Source

**Decision:** Wikipedia was added as a secondary information source.

**Reason:**
- Provides additional background information.
- Helps diversify retrieved research material.
- Complements web search results.

### n8n Data Tables – Research Memory

**Decision:** n8n Data Tables were selected to store previous research records.

**Reason:**
- Provides persistent storage within the automation platform.
- Allows previous research queries to be retrieved.
- Helps the planner use previous research history when generating new search tasks.

### HTML to PDF Service – Report Export

**Decision:** An HTML-to-PDF service was selected for report generation.

**Reason:**
- Converts report content into a shareable PDF format.
- Supports HTML-based report formatting.
- Keeps document generation separate from research and analysis.

## 3. Research Workflow Design

The workflow separates research into independent stages:

1. Query validation.
2. Research planning.
3. Search task generation.
4. Multi-source information retrieval.
5. Webpage content extraction.
6. Source aggregation and deduplication.
7. AI analysis and report generation.
8. Research quality checks.
9. Memory storage.
10. PDF generation.

This modular approach makes individual stages easier to test and troubleshoot.

## 4. Why Data Table Memory Instead of RAG?

The current implementation uses n8n Data Tables to store previous research queries, timestamps, source counts, and generated reports.

A vector database and RAG pipeline were considered as possible future enhancements but were not included in the current implementation.

**Reason for the decision:**
- The assessment version prioritizes a working end-to-end research workflow.
- Structured memory is sufficient for storing and retrieving previous research records.
- Avoids adding unnecessary infrastructure and configuration complexity.

## 5. Reliability and Error Handling

The workflow includes:
- Input validation.
- Retry settings on selected HTTP requests.
- Error-handling paths for search and memory operations.
- Source deduplication.
- Research quality checks for required report sections and source links.

These measures help identify incomplete responses and service failures.

## 6. Known Limitations

- Local LLM performance depends on available hardware.
- Long report generation can be limited by model output capacity and infrastructure timeouts.
- Search quality depends on external information sources.
- The current memory system does not provide semantic vector retrieval.
- Research quality checks use structural conditions and do not independently verify every factual claim.

## 7. Future Improvements

- Add a vector database and RAG-based retrieval.
- Improve report length and generation reliability.
- Add stronger source relevance ranking.
- Implement more advanced factual verification.
- Add monitoring, logging, and more comprehensive failure recovery.
- Improve PDF formatting and report presentation.

## 8. Final Design Philosophy

The project prioritizes modularity, practical automation, cost-conscious LLM usage, multi-source research, and a working end-to-end workflow. The architecture is designed to support future improvements without requiring a complete redesign.
