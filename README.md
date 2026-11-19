# Autonomous AI Research Agent

An AI-powered research agent built using **n8n, Ollama, Tavily Search, and Wikipedia**. It automates research by breaking a query into smaller tasks, collecting information from multiple sources, analyzing the findings, and generating a structured research report.

## Features

- Accepts research queries through a chat interface.
- Uses an LLM to create a research plan.
- Breaks research into multiple search tasks.
- Collects information using Tavily Search and Wikipedia.
- Extracts and combines relevant webpage content.
- Removes duplicate sources and aggregates research findings.
- Uses an LLM to analyze information and generate a report.
- Performs a research quality check.
- Generates a PDF report.
- Stores previous research information using n8n Data Tables.

## Technology Stack

| Technology | Purpose |
|---|---|
| n8n | Workflow automation and orchestration |
| Ollama | Local LLM inference |
| Qwen 3 (1.7B) | Research planning and report generation |
| Tavily Search | Web research |
| Wikipedia | Knowledge retrieval |
| n8n Data Tables | Research memory |
| PDF generation service | Report generation |

## Workflow Overview

1. User submits a research query.
2. The agent validates the query.
3. Ollama generates a research plan.
4. The plan is converted into search tasks.
5. Tavily and Wikipedia collect relevant information.
6. Webpage content is extracted and normalized.
7. Sources are merged, deduplicated, and aggregated.
8. Ollama analyzes the collected information and writes a report.
9. A quality-check step evaluates the report.
10. The workflow generates a PDF and stores research memory.
11. The final output is returned to the user.

## Project Structure

```text
autonomous-ai-research-agent/
├── README.md
├── workflow/
│   └── research-agent.json
├── documentation/
│   ├── architecture.md
│   ├── design-decisions.md
│   └── installation-guide.md
├── sample-runs/
│   ├── successful-run.md
│   ├── second-run.md
│   └── failure-handling.md
└── screenshots/
```

## Setup

1. Install and configure n8n.
2. Install Ollama and download the required model.
3. Configure Tavily API credentials in n8n.
4. Configure the required PDF generation service.
5. Import the workflow JSON into n8n.
6. Set up the required credentials and environment-specific connections.
7. Execute the workflow using a research query.

**Note:** Update the setup instructions with the actual configuration used in this project before deployment.

## Limitations

- Report length and generation time depend on the selected LLM and infrastructure.
- Local model performance depends on available hardware resources.
- External search and webpage extraction depend on third-party service availability.
- The current implementation uses structured workflow memory rather than a full vector-based RAG pipeline.

## Future Improvements

- Integrate vector database-based retrieval.
- Improve long-report generation and PDF formatting.
- Add more research sources.
- Improve error handling and retry mechanisms.
- Add source relevance scoring and stronger fact verification.

## Author

Developed as an autonomous AI research automation project using n8n and open-source LLM technology.
