# SourceMedium for Gemini CLI

Query and analyze the commerce data your organization maintains in SourceMedium, from Gemini CLI. The extension installs SourceMedium's remote MCP server and gives the agent a data-analysis workflow that preserves SourceMedium's metric definitions and data boundaries.

## What it provides

- SourceMedium MCP tools for warehouse, Shopify, Meta Ads, health, catalog, and documentation data.
- OAuth connection through SourceMedium's existing authorization flow, discovered automatically from the server.
- An agent skill that starts with data context, prefers canonical metrics, bounds custom SQL, and reports assumptions.

The server is read-only. It cannot change provider settings, credentials, connections, or warehouse data. No Google Cloud project, `gcloud` login, or BigQuery credential is required: your SourceMedium organization membership determines what the server can reach.

## Install

```bash
gemini extensions install https://github.com/source-medium/sourcemedium-gemini
```

Restart Gemini CLI, then authenticate:

```text
/mcp auth sourcemedium
```

Complete the SourceMedium sign-in and consent flow in the browser. Verify with `/extensions list` and `/mcp`.

An active SourceMedium account is required. If sign-in succeeds but every tool denies access, your user is not yet entitled to an organization; contact your SourceMedium administrator.

## Local development

```bash
gemini extensions validate .
gemini extensions link "$PWD"
```

Restart Gemini CLI and confirm the extension appears in `/extensions list`, the SourceMedium server appears in `/mcp`, and OAuth completes. Unlink the local copy and install from GitHub in a clean environment before tagging a release, so the path a first-time user takes is the one that was tested.

## Data-use workflow

For an analysis session, the agent should first inspect the available data with `get_data_context`, use `search_data_catalog` before querying, and prefer `query_metrics` for SourceMedium-defined metrics. It should only use custom SQL after inspecting the relevant tables and columns, and should state the source, date range, freshness, and assumptions in its answer.

## Support

Documentation: [Connect an AI assistant](https://sourcemedium.com/docs/ai-analyst/connect-an-ai-assistant)

For help, contact [SourceMedium support](mailto:support@sourcemedium.com).
