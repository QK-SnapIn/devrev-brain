---
title: Remote MCP Server
type: feature
status: draft
sources: []
related: ["features/workflows", "features/agents"]
last_updated: 2026-04-12
---

# Remote MCP Server

## What it does
DevRev exposes its platform as a remote MCP (Model Context Protocol) server, allowing external AI agents to call DevRev actions as tools. The server endpoint is `https://api.devrev.ai/mcp/v1`. DevRev also acts as an MCP client — workflows can call external MCP servers as nodes.

## Why it exists
Enables external AI tools and agents to interact with DevRev programmatically via the MCP standard, removing the need for custom integrations. This makes DevRev actions (ticket creation, issue updates, search, etc.) available as first-class tools for any MCP-compatible AI client.

## Key behaviors
- Server URL: `https://api.devrev.ai/mcp/v1`
- Authentication: OAuth (default) or DevRev PAT (Personal Access Token)
- Supported MCP clients: Claude Desktop, Claude Code, OpenAI ChatGPT, GitHub Copilot CLI, Google Gemini, Amazon Quick Suite
- DevRev acts as both an MCP **server** (exposing actions to external agents) and an MCP **client** (workflows can call external MCP servers as nodes)
- Any DevRev workflow can be annotated and exposed as an MCP tool
- Tools exposed follow the MCP standard protocol for discovery, invocation, and response

## Entry points
- External AI agents connect to `https://api.devrev.ai/mcp/v1`
- DevRev workflows can include MCP client nodes to call external MCP servers
- Documentation: https://docs.devrev.ai/product/remote-mcp

## Related flows
[gap] No flow pages yet for MCP setup or MCP tool invocation.

## Related scenarios
[gap] No scenario pages created yet for MCP test cases.

## Open questions
- [gap] What is the full list of DevRev actions exposed as MCP tools?
- [gap] How is OAuth configured for MCP clients — is it standard OAuth 2.0 or DevRev-specific?
- [gap] Are there rate limits specific to MCP server calls?
- [gap] How are workflow-as-MCP-tool annotations configured in the UI?
- [gap] What happens when an external MCP server called by a workflow is unreachable?
