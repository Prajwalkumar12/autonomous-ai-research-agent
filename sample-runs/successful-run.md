# Successful Run – AI Research Agent

## Test Objective

To verify that the AI Research Agent can accept a research query, generate a research plan, retrieve information from multiple sources, analyze the collected content, and produce a structured research report.

## Test Input

- **Research Query:** Research the latest developments in AI automation in 2026. Find 10 useful articles, analyse them, identify important trends and prepare a research report.
- **Execution Date:** 19 November 2026
- **Workflow Platform:** n8n
- **LLM:** Ollama (Qwen 3 – 1.7B)
- **Research Sources:** Tavily and Wikipedia

## Workflow Execution

1. Research query received through the chat trigger.
2. Query validated and previous research memory loaded.
3. Ollama generated a structured research plan.
4. The research plan was parsed into three search tasks:
   - n8n business automation trends 2026
   - AI agents in business processes 2026
   - AI agents and n8n real-world applications
5. Tavily and Wikipedia retrieved relevant information.
6. Results were merged, normalized, and deduplicated.
7. Webpage content was extracted and analyzed.
8. Ollama generated the research report.
9. Research quality check was performed.
10. Research memory was saved.
11. Final output was returned and PDF generation was triggered.

## Execution Results

- **Workflow Status:** Successful execution
- **Sources Retrieved:** 5
- **Research Plan Generated:** Yes
- **Search Tasks Generated:** 3
- **Report Generated:** Yes
- **PDF Generation:** Yes
- **Research Memory:** Saved

## Observations

The workflow successfully demonstrated an end-to-end AI-powered research process, from accepting a user query to generating a structured research report. Combining Tavily web search with Wikipedia helped gather information from multiple sources, while the deduplication and content extraction steps helped organize the collected results before analysis.

The modular workflow made each stage easier to monitor and troubleshoot. Research memory also provides a way to retain previous research outputs for future reference.

One limitation observed was that report length and PDF output can vary depending on the local LLM's response capacity and execution time. This can be improved by optimizing prompts, increasing model capacity, and adding better timeout and output-length handling.




