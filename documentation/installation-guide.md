# Installation and Setup Guide

## 1. Prerequisites

Before setting up the Autonomous AI Research Agent, ensure that you have:

- An n8n account (Cloud or self-hosted).
- Ollama installed on a machine where the model can run.
- Qwen 3 1.7B model downloaded in Ollama.
- A Tavily API account and API key.
- Access to the configured HTML-to-PDF service.
- A configured n8n Data Table for research memory.

## 2. Install Ollama

1. Download and install Ollama from https://ollama.com/.
2. Open a terminal or command prompt.
3. Download the model:

```bash
ollama pull qwen3:1.7b
```

4. Verify that the model is available:

```bash
ollama list
```

5. Ensure that the Ollama API is accessible from the environment where n8n runs.

Default local API endpoint:

```text
http://localhost:11434
```

**Note:** If n8n Cloud is used, localhost on the n8n server does not refer to the user's computer. A secure, reachable endpoint is required. Do not expose an unauthenticated Ollama API publicly.

## 3. Import the n8n Workflow

1. Log in to your n8n account.
2. Open the Workflows section.
3. Select the option to import a workflow from a file.
4. Choose the provided `research-agent.json` file.
5. Verify that all workflow nodes and connections have been imported.

## 4. Configure Tavily Credentials

1. Create or access your Tavily API account.
2. Generate an API key.
3. In n8n, open Credentials.
4. Create an HTTP Header Auth credential.
5. Configure the header required by your Tavily API account.
6. Assign this credential to both:
   - Tavily - Search Web
   - Tavily - Extract Webpage Content

Keep API keys inside n8n Credentials. Never hardcode them in workflow code or publish them in GitHub.

## 5. Configure Ollama HTTP Nodes

Open the following nodes:

- Ollama - Create Research Plan
- Ollama - Analyze and Write Report

Update their HTTP endpoint URLs to the reachable Ollama API endpoint.

The workflow uses the `/api/chat` endpoint and the `qwen3:1.7b` model.

Ensure the endpoint is accessible before executing the workflow.

## 6. Configure Research Memory

1. Open the Data Tables section in n8n.
2. Create a Data Table named `ResearchMemory`.
3. Add these columns:

| Column | Type |
|---|---|
| researchQuery | String |
| generatedAt | String |
| sourceCount | Number |
| reportMarkdown | String |

4. Open the Load Previous Research Memory and Save Research Memory nodes.
5. Select the newly created `ResearchMemory` table in both nodes.

## 7. Configure PDF Generation

1. Ensure the required HTML-to-PDF service is available.
2. Configure its API credentials in n8n.
3. Open the Convert HTML to PDF node.
4. Select the configured PDF service credential.
5. Verify that the service can generate a PDF successfully.

## 8. Test the Workflow

1. Save the imported workflow.
2. Execute or activate the workflow as required by the n8n Chat Trigger configuration.
3. Submit a research topic.
4. Verify that the agent creates research queries.
5. Check that Tavily and Wikipedia return information.
6. Verify that the report is generated.
7. Confirm that research memory is saved.
8. Verify PDF generation.

## 9. Troubleshooting

| Issue | Suggested Check |
|---|---|
| Ollama connection failed | Verify the API endpoint, model and network access |
| Tavily authentication failed | Check the HTTP Header Auth credential |
| No search results | Check query input and Tavily connectivity |
| Memory not saved | Verify the Data Table and column mapping |
| PDF generation failed | Check PDF service credentials and availability |
| Incomplete report | Check model output limits and generation time |

## 10. Security Notes

- Never commit API keys, passwords or tokens to GitHub.
- Store credentials using n8n Credentials.
- Use secure network access for Ollama.
- Replace example endpoints with your own configured endpoint.
- Review workflow exports before publishing them.

## 11. Important Note

This guide describes the configuration required to run the workflow. Exact endpoint URLs, credentials and service availability depend on the deployment environment.
