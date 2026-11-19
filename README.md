# Autonomous AI Research Agent

An AI-powered research automation system built using **n8n, Ollama, Qwen 3, Tavily Search, and Wikipedia**. The agent automates the research process by understanding a user query, generating a research plan, collecting information from multiple sources, analyzing the findings, and producing a structured research report with PDF output.

## Project Overview

The Autonomous AI Research Agent is designed to reduce the manual effort involved in researching a topic.

Instead of manually searching multiple websites and organizing information, users can submit a research query through the chat interface. The workflow then plans the research, retrieves relevant information, processes the collected content, and generates a final report.

The project combines workflow automation, local LLM inference, web search, knowledge retrieval, and structured research memory.

## Key Features

- **Conversational Research Input:** Accepts research queries through an n8n chat interface.
- **AI Research Planning:** Uses Ollama and Qwen 3 to generate a structured research plan.
- **Task-Based Search:** Converts the research plan into smaller search tasks.
- **Multi-Source Research:** Retrieves information using Tavily Search and Wikipedia.
- **Webpage Content Extraction:** Extracts relevant content from selected webpages.
- **Source Processing:** Merges, normalizes, deduplicates, and aggregates research results.
- **AI Report Generation:** Uses an LLM to analyze collected information and prepare a structured report.
- **Research Quality Check:** Includes a quality-check stage before returning the final output.
- **PDF Generation:** Sends the final report for PDF generation.
- **Research Memory:** Uses n8n Data Tables to store previous research information for future reference.

## Technology Stack

| Technology | Purpose |
|---|---|
| n8n | Workflow automation and orchestration |
| Ollama | Local LLM inference |
| Qwen 3 (1.7B) | Research planning and report generation |
| Tavily Search | Web search and information retrieval |
| Wikipedia | Knowledge retrieval |
| n8n Data Tables | Structured research memory |
| HTML-to-PDF Service | PDF report generation |

## Workflow Architecture

The workflow follows a modular research pipeline:

1. **Research Input:** User submits a query through the chat trigger.
2. **Query Validation:** The system validates the incoming research query.
3. **Memory Retrieval:** Previous research information is loaded from n8n Data Tables.
4. **Research Planning:** Ollama generates a structured research plan.
5. **Task Parsing:** The research plan is converted into individual search tasks.
6. **Information Retrieval:** Tavily Search and Wikipedia collect relevant information.
7. **Content Processing:** Search results are normalized, merged, and deduplicated.
8. **Webpage Extraction:** Relevant webpage content is extracted for deeper analysis.
9. **AI Analysis:** Ollama analyzes the collected research material and generates a report.
10. **Quality Check:** The generated report passes through a research quality-check stage.
11. **Memory Storage:** Research information is saved in n8n Data Tables.
12. **Final Output:** The report is returned to the user and PDF generation is triggered.

## Repository Structure

```text
autonomous-ai-research-agent/
│
├── README.md
│
├── workflow/
│   └── research-agent.json
│
├── documentation/
│   ├── architecture.md
│   ├── design-decisions.md
│   └── installation-guide.md
│
└── sample-runs/
    └── successful-run.md
```

## Installation and Setup

### Prerequisites

- n8n (Cloud or self-hosted)
- Ollama installed and running
- Qwen 3 (1.7B) model
- Tavily API key
- Configured PDF generation service
- Required n8n credentials and Data Tables

### Setup Steps

1. Install and configure Ollama.
2. Download the required model:

   ```bash
   ollama pull qwen3:1.7b
   ```

3. Start Ollama and verify that its API is accessible.
4. Configure a reachable Ollama endpoint in the n8n workflow.
5. Add Tavily API credentials in n8n.
6. Configure the PDF generation service credentials.
7. Import `workflow/research-agent.json` into n8n.
8. Configure the required Data Tables and their columns as described in the installation guide.
9. Verify all node connections and credentials.
10. Execute the workflow using a research query.

For detailed configuration instructions, refer to:

**[Installation Guide](documentation/installation-guide.md)**

**[Architecture Documentation](documentation/architecture.md)**

**[Design Decisions](documentation/design-decisions.md)**

> Important: If n8n Cloud is used with a locally hosted Ollama instance, the Ollama API must be accessible through a secure, reachable endpoint. Do not expose an unauthenticated Ollama API publicly.

## Sample Execution

A sample successful execution is documented here:

**[Successful Research Run](sample-runs/successful-run.md)**

The sample run demonstrates the research workflow, information retrieval, report generation, and PDF generation stages.

## Limitations

- Report length and generation time depend on the selected LLM and available infrastructure.
- Local model performance depends on hardware resources.
- External search and webpage extraction depend on third-party service availability.
- PDF output can vary depending on LLM response length and execution time.
- The current implementation uses structured workflow memory through n8n Data Tables rather than a full vector-based RAG pipeline.

## Future Improvements

- Integrate a vector database for semantic retrieval and advanced RAG.
- Improve long-form report generation and PDF formatting.
- Add more research sources and search providers.
- Implement stronger error handling
