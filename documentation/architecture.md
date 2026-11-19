# System Architecture

## Overview

The Autonomous AI Research Agent is an automated research workflow built using n8n. It accepts a research query, creates a research plan, collects information from multiple sources, analyzes the collected content, and generates a structured research report.

## Architecture Components

### 1. User Input
- Research Chat Trigger receives the user's research topic.
- Validate Research Query checks that the input is not empty.

### 2. Research Planning
- Previous research records are loaded from the ResearchMemory Data Table.
- Ollama (Qwen 3 1.7B) generates a research goal and search queries.
- Parse Plan into Search Tasks converts the generated queries into individual tasks.

### 3. Information Retrieval
The workflow retrieves information from two sources:

- **Tavily Search:** Searches the web for relevant information.
- **Wikipedia:** Retrieves relevant knowledge-base search results.

### 4. Content Processing
- Tavily Extract retrieves webpage content for selected URLs.
- Search and extracted results are normalized and merged.
- Duplicate URLs are removed.
- Source information is aggregated for analysis.

### 5. AI Analysis and Report Generation
- Ollama analyzes the collected research information.
- The model generates a Markdown report with sections such as Executive Summary, Research Plan, Key Findings, Important Evidence, Actionable Insights, Limitations, and Sources.
- Research Quality Check checks required sections, source links, and report length.

### 6. Memory Management
- Previous research records are loaded from the n8n Data Table.
- Completed research information is saved in the ResearchMemory table.
- Memory status is included in the final output.

### 7. PDF Generation
- The final report content is converted into HTML.
- The HTML-to-PDF service generates the PDF report.

## High-Level Workflow

```text
User Research Query
        |
        v
Input Validation
        |
        v
Load Previous Research Memory
        |
        v
Ollama Research Planner
        |
        v
Search Task Generation
        |
        +----------------------+
        |                      |
        v                      v
   Tavily Search          Wikipedia Search
        |                      |
        +----------+-----------+
                   |
                   v
          Merge Search Results
                   |
                   v
          Extract Webpage Content
                   |
                   v
        Deduplicate and Aggregate
                   |
                   v
          Ollama Research Analyst
                   |
                   v
          Format Research Report
                   |
                   v
          Research Quality Check
                   |
                   v
           Save Research Memory
                   |
                   v
           Return Final Output
                   |
                   v
             Generate PDF
```

## Data Flow

1. The user's query enters the workflow through the chat trigger.
2. The planner uses the query and available previous research history to create search tasks.
3. Search tasks are processed through Tavily and Wikipedia.
4. Retrieved information is extracted, merged, and deduplicated.
5. The AI analyst uses the collected information to generate a structured report.
6. The report passes through a quality-check step.
7. Research data is saved in the ResearchMemory Data Table.
8. The final result is returned and converted into a PDF.

## Architecture Notes

- n8n handles workflow orchestration and data movement.
- Ollama runs the language model inference through an HTTP API endpoint.
- Tavily and Wikipedia provide external research information.
- n8n Data Tables provide persistent research history.
- The PDF service converts the generated report into a downloadable document.

## Current Limitations

- Report length depends on the local LLM's generation capacity and available resources.
- External search and webpage extraction depend on third-party services.
- The current memory implementation uses n8n Data Tables and does not implement vector-based retrieval.
- PDF generation depends on the configured external PDF service.
