---
title: MCP integration
type: developer-doc
status: stable
source: developer.devrev.ai
category: airsync
source_url: https://developer.devrev.ai/airsync/mcp
last_updated: 2026-05-11
summary: "The Model Context Protocol (MCP) is an open protocol that enables large language models to interact with applications through standardized interfaces."
---

# MCP integration

MCP integration

The Model Context Protocol (MCP) is an open protocol that enables large language models to interact with applications through standardized interfaces.

Chef-cli provides MCP integration through the `chef-cli mcp initial-mapping` subcommand.
This integration allows AI assistants to programmatically edit and test initial domain mapping files.

## [Limitations](#limitations)

MCP integration is experimental. Functionality may vary across different AI
models and MCP clients.

Cursor and Claude Code demonstrate reliable performance with this integration. AI assistants can prepare initial domain mappings with significant autonomy, though developer oversight remains essential.

## [Prerequisites](#prerequisites)

* Chef-cli installed and configured
* MCP-compatible client (Cursor, Claude Code, etc.)
* External domain metadata file

## [Configuration](#configuration)

Create a `mcp.json` file with the following content:

```
{
  "mcpServers": {
    "AirSync": {
      "command": "chef-cli",
      "args": ["mcp", "initial-mapping"]
    }
  }
}
```

### [Set up Cursor](#set-up-cursor)

1. Place `mcp.json` in your project's `.cursor` directory (at `<project-root>/.cursor/mcp.json` for project-level config, or `~/.cursor/mcp.json` for user-level config).
2. Restart Cursor.
3. Specify the initial domain mapping file location in **Agent mode**.
   a. Use absolute file paths for optimal results.
   b. Alternatively, provide an existing initial domain mapping file.
4. Direct the AI to create the initial domain mappings.
5. Run `initial-mapping check` to validate initial domain mappings against the local domain metadata file.

Add DevRev's AirSync documentation to your MCP server by including `https://developer.devrev.ai/public/airsync/` as a custom docs URL.

See [Cursor documentation](https://cursor.com/docs/context/symbols#docs) for details.

### [Claude Code setup](#claude-code-setup)

1. Run `claude mcp add airsync chef-cli mcp initial-mapping`.
2. Start Claude Code.
3. Specify the initial domain mapping file location.
   a. Alternatively, provide an existing initial domain mapping file.
4. Direct the AI to create the initial domain mappings.
5. Run `initial-mapping check` to validate initial domain mappings against the local domain metadata file.

### [Other IDEs](#other-ides)

You can use the same `mcp.json` file in other IDEs that support MCP servers.

## [Usage guidelines](#usage-guidelines)

Provide these instructions to your AI assistant when using the MCP server:

```
When performing AirSync initial mapping:

- Use `metadata.json` for external domain metadata.
- Use `mappings.json` as the initial domain mapping file.
- Call `use_mapping` to test how the initial mapping behaves on the current metadata.
- Use MCP tools for:
  - Adding and removing record type mappings
  - Unmapping fields
  - Mapping simple fields
- For complex field mappings, edit the mapping file directly:
  - Refer to `initial_mappings_schema.yaml` for proper format.
  - Always call `use_mapping` to verify the mapping file remains valid.
```

Adjust file paths according to your project structure.

## [Available operations](#available-operations)

The MCP server provides the following tools:

* Test mappings against metadata files
* Add and remove record type mappings
* Map and unmap fields
* Validate mapping file structure

Last updated on

[Publish to the marketplace

Previous Page](/airsync/publish-to-marketplace)[Common issues

Next Page](/airsync/faq)

## Source
- DevRev developer docs: [MCP integration](https://developer.devrev.ai/airsync/mcp)
